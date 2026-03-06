# To Do

13 predictions: these were on the strains that did not have any clue by the other methods.
	- 11/13 did not have acc. plasmid
	- 2 predictions had 4 and 5.
	- [ ] RFPlasmid might be showing that 5-mers are not enough to see acc. pls.
		- [ ] Is it worthy to move to more -mer based tools like Plasmer? Let's first check the k-mer distributions between acc. plasmids and psyms/chromosomes.
			- Based on their results with 31k bacterial genomes plasmids find a better kmer sharing at 25-mer, whereas chromosomes at a 18 k-mer.

# Table of Content

```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
include: 
exclude: 
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

# About this project

This is an extension of [[Plasmid prediction in illumina MAG strains]], but now focus on enhancing the strategy for accessory plasmid prediction in *Sinorhizobium meliloti.

The strategy will consist of prepare a pipeline including all the data learned in the past.

In summary, during the mentioned document we learned that the accessory plasmids and the mega-plasmids share giant amounts of DNA. Therefore, it is clear that the more fragmented a genome, the harder it will be to distinguish between an accessory plasmid and a mega-plasmid. 

Several tools with(out) Machine learning techniques were applied, but they were not good at all. It is clear that a mixed of them is needed and some of them are actually a mix ([[Plasmid prediction in illumina MAG strains]]). However, they were made to distinguish between chromosome and plasmid, and the assumptions in the difference between a chromosome and plasmid are higher than between a mega-plasmid and a acc. plasmid. 


RFPlasmid was the only tool I found trainable, and according to a recent [benchmarking](https://doi.org/10.1093/bib/bbaf589) between different plasmid prediction tools (RFPlasmid is integrated in PlasmidEC), RFPlasmid with Plasmer was among the best. 

![[benchmarking_pls_tools.jpeg]]


Plasmer has my favorite strategy, unfortunately, it is not trainable, so I will try to replicate a similar work and produce a tool to train using our database of Sinorhizobium meliloti accessory plasmids.

# First insights 

We now know that using markers and short kmers is not enough to correctly predict accessory plasmid in the presence of mega-plasmids like in *Sinorhizobium meliloti* 

One exploratory analysis is observe sequence separation with higher k-mer number such as during Plasmer paper. 

The data was split into: 
1. Chromosome:Contains pSyms and Chromosome
>Folder: /n/projects/jp2992/plasmid_prediction/kmer_plotting/chromosome_fastas_slide_10kb

2. Accessory Plasmids: These are all the plasmids less than 500 kb from the PLSDB for *S. meliloti*
>Folder: /n/projects/jp2992/plasmid_prediction/kmer_plotting/plasmids_fastas_slide_10kb

## Count kmer with KMC

I used KMC for k-mer counting, as it does not handle multiple fasta files nor multi-fasta, because KMC returns only one matrix, I had to do array job, to count on each window as I have thousands.

> /n/projects/jp2992/plasmid_prediction/code/slurm_master_KMC.sh


The idea is count 25-mer. I am using *Plasmer* research as reference, since they investigated the best plasmid kmer size for a maximal separation between chromosome and plasmids. 25-mer was one of the best values.

However, I am noticing that as expected using 25-kmer will not be as easy as thought. Below is a UMAP projection using 50 PC from the 25-mer composition of 2k windows of 10kb:

![[umap_25mer_chr_pls.png]]

We can see that we can cross an horizontal line between pls and chr. Although, several windows overlap between them maybe can be enough to detect and not to reconstruct. Here a step like in *Plasmer*, remove the shared kmers, can improve the strategy. 

**TODO** One interesting thing to use is the GC content. I have found for example that during the predictions on penn state assemblies the fragmented assemblies presents predictions highly likely to be false positive because the sizes are very small Q3: 16313.00 and the GC content very high > 61-63%. Although we can find small sizes with lower GC values. 

In the previous, the Chr represents the pSyms + Chromosome, now let's look only at pSyms vs Accessory plasmids.

## Counting kmer with Sourmash

I tried to compare chromosome/psymAB vs Acc. plasmid. The problem is that here the comparisons are between signatures and not all vs all. I think this limits my resolution. Additionally, in sourmash I consider sketches with scale=100 otherwise I think it would be very slow. Another aspect to point is that the chromosome/psymAB presented higher sampling. Although that was my fault. In the next attempt with kmer-db I will separate each contig. **I prefer kmer-db over Sourmash since it is faster, I can create all kmer comparison, and Sourmash implies creating a signature for each sample to be abled to do all vs all comparison**.

chromosome-psym: 9359 // plasmid: 641

![[sourmash_PCoA.png]]


![[sourmash_distance_UMAP.png]]

## Counting kmer with kmer-db

I noticed during a k-mer counting of Ori for siva, that these can be unique enough to separate all contigs. However, I was using only 44 strains. I will try a 20mer counting again using 10kb, 30kb and 50kb windows.

>Files path
>/n/projects/jp2992/plasmid_prediction/kmer_plotting/in_house_approach

| file             | num_seqs | sum_len     | min_len   | avg_len     | max_len   |
| ---------------- | -------- | ----------- | --------- | ----------- | --------- |
| chromosome.fasta | 44       | 163,572,287 | 3,555,948 | 3,717,552   | 3,958,706 |
| psymA.fasta      | 44       | 62,780,448  | 1,213,978 | 1,426,828.4 | 1,692,964 |
| psymB.fasta      | 44       | 73,121,028  | 1,590,727 | 1,661,841.5 | 1,721,762 |

The kmer-db output is a horrible lower-triangle, i.e only the values below the diagonal are filled. For this Eric Ross help me with a [script](/n/projects/jp2992/plasmid_prediction/code/parse_kmer_db.py) to parse the CSV file with the common kmers.

Comparison using sliding window of 10kb, 30kb and 50 kb with a 90% overlapping revealed the expected, for 10kb the plasmids sequences are hardly discriminate using cosine distance based on the allvsall common 20mers, in 30kb they start being separable (image below), and of course 50kb represents the best scenario. 

![[10kb_20mer.png]]

![[30kb_20mer.png]]

Increment to 28mer created a slight improvement. However, I doubt increasing kmer might be a good solution considering the computational cost associated to big kmer sizes.

![[10kb_28mer.png]]


> [!QUESTION]
> **A small detour:** I have a stupid idea in the head. can we use only the putative ori to cluster accessory plasmids? or can we use this to infer similar ancestors? can we detect kmer perturbations compared with this to detect HGT or insertions
> For the last question there is a problem with OriV. First, so far, not all accessory plasmids can be predicted with OriV as it depends on the IGS database in PlasAnn, and second, I doubt the OriV is assembled in short read assembly due to its repeat nature.





