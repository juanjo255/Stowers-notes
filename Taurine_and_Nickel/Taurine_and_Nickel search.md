
To get have a good sensitivity I will use the Tau[ABCD] in 1021 to look for similars in all complete S. meliloti strains using **MMSeqs2** and build a database to look for those proteins in the other nodule bacteria.

# Tasks

1. Search for the TauA (gene) and nickel (promoter y gene) in the Rhizobiaceae, including our Sinorhizobium strains.  ✅
2. Make a phylogenetic tree of all the bacteria used, paint those presenting the Tau.  ✅
3. Make a phylogeny tree of all the bacteria found, paint those presenting the nickel promoter.  ✅ 
4. How many genomes above 70% coverage.   ✅
5. How many genomes above 40% coverage  ✅
6. Venn diagram between genomes in nickel and TauA   ✅
7. Add names to the graph like genus. ✅
8. How many total sinorhizobium meliloti strains and how many carrying the tauA and nickel.✅

# Methods

## Data acquisition (genomes)
 
 All the genomes of the family *Rhizobiaceae* were downloaded from RefSeq. Therefore, here I am using all species and strains with high-quality genomes. 

> Download genomes command:
> `datasets download genome taxon "Rhizobiaceae" --include genome,protein,gbff --assembly-source "RefSeq"`

## Gene Search
 
 *MMseqs2* in PSI-BLAST-like way was used to search for the TauA and Nickel. I consider a e-value of 1e-5 for BLASTP-like search and evalue of 1e-3 for profile construction and only 2 iterations.
> Command:
> /n/projects/jp2992/paco_taurine/code/slurm_create_PhyloTree.sh

  
## Phylogenetic Tree Constrution

 In parallel, I tried three approaches for the phylogenetic tree:
	1. 16rRNA were extracted with `barrnap` and `IQTREE` was used to create the phylogenetic tree.
	2. Tree with Mash distances using `Mashtree`. It is not a phylogenetic tree itself maybe more a dendrogram of a matrix of similarities, but I think it might be good enough to represent.
	3. Neighbor-Join (NJ) by MAFFT: It doesn't perform phylogenetic inference. but It can work well to show distances relations. This was performed using MAFFT website and using the 16S-rRNA retrieved from barrnap (**preferred**).


> Command Barrnap + IQTREE: 
`> /n/projects/jp2992/paco_taurine/code/create_fast_phylogenetic_tree.sh`
> Command mashtree: 
`> /n/projects/jp2992/paco_taurine/code/create_fast_phylogenetic_tree.sh`



# Results

## TauA and Nickel genes search

![[tauA_Nickel_search.png]]

In the plot we can observed the distribution of coverage (tcov) and identities (findent) recovered with `MMseqs2`.The table below show the number of genomes found with the respective gene.

| Gene   | # genomes | > 40% | >70% |
| ------ | --------- | ----- | ---- |
| TauA   | 3115      | 3082  | 2862 |
| Nickel | 1109      | 1108  | 1079 |
| Total  | 3308      | -     | -    |





## Phylogenetic Tree

The method selected was *NJ by MAFFT* (check methods) as it is the fastest and as the branch lengths are not attach to genomic distance, it produces artificial branch lengths with leaves at the same level, perfect for a pretty plot with the differences in the genes matches (cov and id). The other trees can be tuned to ignore the branch lengths, so the selection was just aesthetic. Mashtree produces too populated branches. On the other hand, IQTREE honestly looks very weird.

> Tree file:
> /n/projects/jp2992/paco_taurine/NJ_rhizobiaceae_16S_rRNA.on.nh


> [!NOTE]
> 
> *Barrnap* did not find the 16rRNA is all genomes. So I used only those with it, for a total of  3,190 out of 3,308
> 
>16S-RNA:
> /n/projects/jp2992/paco_taurine/rhizobiaceae_16SrRNA_2.fasta 

Example of the tree:
![[example_tree_rhizobiaceae.svg]]

The tree was plotted in *iTOL*, it is a private website, but the free features are good enough, also it is very easy to use. *TreeViewer* is an open source app alternative.

To add the colors as in the image you need some metadata files (CSV).
>Metadata folder for iTOL:
>/n/projects/jp2992/paco_taurine/iTOL_metadata/


All the trees plotted can be found at:
>Tree plotted:
>>/n/projects/jp2992/paco_taurine/iTOL_trees_plots/
