# Tasks 📋

* Annotate and extract origin of replication in pSymA, pSymB and accessory ✅ 
* Make a sequence comparison: kmer composition might be relevant in a guide RNA scenario ✅

# Annotation of OriV 📚


In plasmids the origin of replication is known as OriV, the equivalent to chromosomes OriC. Annotating OriV presents some challenges compared to the chromosome. Since plasmids has high gene content variability a classical GC skew strategies cannot be used. Likewise, the conservation between plasmids is very low, the latter coupled with a low number of OriV entries, hinders BLAST-based approach. However, fortunately for us, the RepABC is a popular replication module, so we might have good anchors to find for the OriV.

OriV has been described to be present within the intergenic sequences (IGSs) adjacent to the genes encoding replication initiation proteins (RIPs) and in some cases has been observed embedded within these genes. In Sinorhizobium meliloti's plasmids RepC is very common and widely annotated. 

Currently, for OriV annotation I have found three strategies:
1. OriV-Finder/Ori-Finder: it uses RIP proteins, and subsequently it looks for AT-rich and GC-rich changes. 
2. BAKTA: It uses BLAST to search against the DoriC.
3. PlasAnn: Probably the best option. it is the most recent released tool. It is specialized in plasmid annotation, including OriV/OriC/OriT, for Oriv annotation they replicated OriV-Finder strategy. 

# Method 🧰

For this first analysis, I used only the strains sequenced in house as these represents very high quality assemblies and some of the MAG strains relevant for the lab.

From the previous strategies, BAKTA and PlasAnn are open-source, which allow us to perform high throughput analysis of OriV. 

BAKTA will help us get the chromosomal Ori, whereas PlasAnn represents the best option to get Psyms and accessory plasmids Ori. 

Once the putative Oric/V regions were retrieved, we conducted k-mer composition analysis at lengths of 6 bp and 20 bp. The 6-mer analysis aimed to look for differences in local sequence composition, for instance due to GC content or repeats. The 20-mer analysis, relevant to the potential design of guide RNAs, was used to assess whether motif compositions differ sufficiently between all replicons.

# Results 📊

BAKTA successfully annotated Ori regions across all chromosomes and, interestingly, nearly all pSymA replicons. However, no Ori regions were detected in any pSymB replicons. Although pSymA and pSymB were annotated by PlasAnn, for the comparison purposes I've included the BAKTA annotation results for pSymA.


| File                          | num_seqs | sum_len | min_len | avg_len | max_len | source  |
| ----------------------------- | -------- | ------- | ------- | ------- | ------- | ------- |
| acc_pls_ori/acc_pls_ori.fasta | 35       | 6,382   | 153     | 182.3   | 211     | PlasAnn |
| chr_ori/chr_ori.fasta         | 44       | 17,776  | 404     | 404     | 404     | BAKTA   |
| psymA_ori/psymA_ori.fasta     | 43       | 86,753  | 1,985   | 2,017.5 | 2,049   | BAKTA   |
| psymB_ori/psymB_ori.fasta     | 0        | 0       | 0       | 0       | 0       |         |


## K-mer composition comparison

**6-mer composition**
Below we can observed a PCA plot using 6-mer composition for all Oris retrieved:

![[pcoa_6-mer_ori_pls_jaccard.png]]
**20-mer composition**

Below we can observed a PCoA plot using distance matrix computed using Jaccard from the 20-mer composition of all Oris retrieved:



![[pcoa_20-mer_ori_pls_jaccard.png]]

However, the plot before was using the Ori annotation for pSymA returned by BAKTA which uses the reference in DoriC, for which there are available only 4 entries.

When we replace the site for the one predicted by PlasAnn, the relationship between pSymA and Acc. plasmids changes:

![[pcoa_20-mer_ori_pls_jaccard_psymAPlassAnn.png]]

Now we can observe how pSymA and Acc. plasmids overlaps indicating similar variation captured from the Jaccard distances, nonetheless if we check the first 5 PCs we can observed pSymA and Acc. plasmid can achieve a level of separation:

![[PCoa1to5_20-mer_ori_pls_jaccard.png]]


And if we integrate the first 4 PCs into a UMAP projection, The 20-mer composition shows structured variation across amplicons, and dimensionality reduction methods reveal separable patterns consistent with divergent k-mer content:

![[umap_PCoA_1_4_20-mer.png]]

