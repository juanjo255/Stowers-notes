
# To Do:

- [ ] Build a genome map of annotation for accessory plasmids:
	- Build plasmidome with ppanggolin **(done)**.
	- The idea is to show an artificial genome built by the plasmids. 
- 
- [ ] re-cluster now adding the MAG and highlight all the clusters where all the new plasmids fall.
	- Plot in scatter plot highlighting the new plasmids **(done)**.
	- Run horizontal gene transfer 80 cov and 80 id.


- [ ] Make homology network colored by the clusters of MGE-Cluster and highlight the MAG and the penn state plasmids. Steps:
	1. I have to download the recent complete MAG: **These genomes I must rename them as they are standard as in the NCBI**. This means that I have to replace the GCA code by the contig code. For this I use `seqkit split` to keep notation.
	2. Annotate plasmids with prodigal to keep consistency (as I annotate the PLSDB with these ones).
	3. Highlight the new plasmids **(done)**.
	4. Add the information from mge_cluster to the homology network **(done)**.



# Objective

PsymA for years has been consider a biggest hotspot for intra-strain variability and accessory gene acquisition by horizontal gene transfer, however it has been found that S. meliloti can also carry accessory plasmids, plasmids that have been proven to also carry competence genes affecting symbiosis. 

During this project we will collect all the accessory plasmids available for S. meliloti and their relatedness with other found in the Rhizobiome.


# Pre-processing

The PLSDB 2024v2 was downloaded and filtered for only sequences below 500Kb.

<details>
<summary> Show command </summary>
```
path=/n/projects/jp2992/MOLNG4331/biocomp_tools/plsdb

seqkit seq -M 500000 $path/plsdb_2025.fasta -o $path/plsdb_less_500kb_2025.fasta

```
</details>

A study [1] presented *Core OTUs found within nodule communities across sampling design, an OTU was defined as core if present in >50% nodule samples*

| OTU ID   | % Samples containing | Phylum              | Class                    | Order                   | Family                 | Genus              |
| -------- | -------------------- | ------------------- | ------------------------ | ----------------------- | ---------------------- | ------------------ |
| Otu00001 | 100.00%              | Proteobacteria(100) | Alphaproteobacteria(100) | Rhizobiales(100)        | Rhizobiaceae(100)      | Ensifer(100)       |
| Otu00004 | 100.00%              | Proteobacteria(100) | Gammaproteobacteria(100) | Alteromonadales(100)    | Shewanellaceae(100)    | Shewanella(100)    |
| Otu00002 | 93.10%               | Proteobacteria(100) | Gammaproteobacteria(100) | Oceanospirillales(100)  | Halomonadaceae(100)    | Halomonas(100)     |
| Otu00034 | 82.76%               | Proteobacteria(100) | Gammaproteobacteria(100) | Oceanospirillales(100)  | Halomonadaceae(100)    | Halomonas(100)     |
| Otu00003 | 75.86%               | Proteobacteria(100) | Gammaproteobacteria(100) | Pseudomonadales(100)    | Pseudomonadaceae(100)  | Pseudomonas(100)   |
| Otu00007 | 68.97%               | Proteobacteria(100) | Betaproteobacteria(100)  | Burkholderiales(100)    | Comamonadaceae(100)    | unclassified(100)  |
| Otu00371 | 68.97%               | Proteobacteria(100) | Alphaproteobacteria(100) | Rhizobiales(100)        | Rhizobiaceae(100)      | Ensifer(100)       |
| Otu00005 | 65.52%               | Proteobacteria(100) | Gammaproteobacteria(100) | Pseudomonadales(100)    | Pseudomonadaceae(100)  | Pseudomonas(100)   |
| Otu00006 | 65.52%               | Proteobacteria(100) | Betaproteobacteria(100)  | Burkholderiales(100)    | Comamonadaceae(100)    | Rhizobacter(88)    |
| Otu00026 | 65.52%               | Proteobacteria(100) | Alphaproteobacteria(100) | Rhizobiales(100)        | Bradyrhizobiaceae(100) | Bradyrhizobium(86) |
| Otu00030 | 62.07%               | Proteobacteria(100) | Alphaproteobacteria(100) | Rhizobiales(100)        | Rhizobiaceae(100)      | Rhizobium(100)     |
| Otu00019 | 58.62%               | Proteobacteria(100) | Betaproteobacteria(100)  | Burkholderiales(100)    | Comamonadaceae(100)    | Rhizobacter(98)    |
| Otu00028 | 55.17%               | Bacteroidetes(100)  | Sphingobacteriia(100)    | Sphingobacteriales(100) | Chitinophagaceae(100)  | Niastella(100)     |
| Otu00010 | 51.72%               | Firmicutes(100)     | Bacilli(100)             | Bacillales(100)         | Planococcaceae(97)     | Solibacillus(85)   |
| Otu00084 | 51.72%               | Bacteroidetes(100)  | Cytophagia(100)          | Cytophagales(100)       | Cytophagaceae(100)     | Ohtaekwangia(100)  |



Additionally, the study performed metagenomic sequencing to study the genome-wide similarity of Ensifer:

> [!NOTE]
> "Because _Ensifer_ was the dominant taxon in all compartments, and MED analysis at the 16S rRNA gene indicated minimal diversity within _Ensifer_ OTUs (see above), we used metagenomic shotgun sequencing to further examine genome-wide similarity of _Ensifer_ populations across different compartments. _Ensifer_ scaffolds reconstructed from root endophyte and nodule communities had, on average, 99% global sequence identity in homologous regions—suggesting that _Ensifer_ are extremely similar throughout an individual plant. Moreover, our estimate of the fraction of _Ensifer_ cells containing each of the two symbiotic megaplasmids did not significantly differ between plant compartments (_W_ = 132, _P_ = 0.10 for pSMED01; _W_ = 151, _P_ = 0.14 for pSMED02; Fig. [4](https://link.springer.com/article/10.1186/s40168-020-00915-9#Fig4))—again suggesting that _Ensifer_ are highly similar throughout the plant, including at the symbiosis megaplasmids."

A review [5] focused on nonrhizobial bacteria usually found within nitrogen-fixing nodules. 

`Table 1: Nonrhizobial nodule-inducing bacterial endophytes isolates from legume root nodules`

| Phylum/class             | Bacterial genus  | nod gene similarity                           |
| ------------------------ | ---------------- | --------------------------------------------- |
| **Alpha-Proteobacteria** | Agrobacterium    | *Ensifer/Rhizobium*                           |
| **Alpha-Proteobacteria** | Aminobacter      | *Mesorhizobium symbiovar loti*                |
| **Alpha-Proteobacteria** | Bosea            | *Mesorhizobium*                               |
| **Alpha-Proteobacteria** | Devosia          | *Rhizobium tropici*                           |
| **Alpha-Proteobacteria** | Methylobacterium | *Burkholderia tuberum*                        |
| **Alpha-Proteobacteria** | Microvirga       | *Rhizobium*, *Bradyrhizobium*, *Burkholderia* |
| **Alpha-Proteobacteria** | Ochrobactrum     | *Rhizobium*                                   |
| **Alpha-Proteobacteria** | Phyllobacterium  | *Mesorhizobium*                               |
| **Alpha-Proteobacteria** | Shinella         | *Rhizobium tropici*                           |
| **Beta-Proteobacteria**  | Burkholderia     | *Burkholderia*                                |
| **Beta-Proteobacteria**  | Cupriavidus      | *Burkholderia*                                |
| **Gamma-Proteobacteria** | Pseudomonas      | *Mesorhizobium*                               |
| **Actinobacteria**       | Rhodococcus      | *Mesorhizobium*                               |

Additionally, they reported some bacteria nonnodulating found in nodules. I select only reported in Medicago: 

| Phylum                   | Bacterial genus |
| ------------------------ | --------------- |
| **Firmicutes**           | Paenibacillus   |
| **Actinobacteria**       | Micromonospora  |
| **Alpha-Proteobacteria** | Azospirillum    |

Another study [6] presented the following families for M. truncatula:

However, considering families can be a problem because it will implied a giant number of plasmids which will be problematic to process

| Family              |
| ------------------- |
| Bradyrhizobiaceae   |
| Phyllobacteriaceae  |
| Rhizobiaceae        |
| Pseudomonadaceae    |
| Sphingomonadaceae   |
| Mycobacteriaceae    |
| Burkholderiaceae    |
| Rhodobacteraceae    |
| Methylobacteriaceae |
| Alcaligenaceae      |
| Xanthomonadaceae    |
| Enterobacteriaceae  |
| Rhodospirillaceae   |
| Streptomycetaceae   |
| Caulobacteraceae    |

Another study [7] proposes the following accessory genuses in M. sativa:

| Genus                |
| -------------------- |
| Arthrobacter         |
| Bacillus             |
| Brevibacillus        |
| Enterobacter         |
| Escherichia_Shigella |
| Lysinibacillus       |
| Nocardioides         |
| Paenibacillus        |
| Pantoea              |
| Pseudomonas          |
| Rhizobium            |
| Streptococcus        |
| Streptomyces         |
| Tumebacillus         |
|                      |


*These results lend support to the idea that in addition to nitrogen fixation, legume root nodules are sites of active antimicrobial production.*


in this study [8] using 16S the researches found the following genus:

| Genus/Group             |
| ----------------------- |
| Sinorhizobium/Ensifer   |
| Rhizobium/Agrobacterium |
| Mesorhizobium           |
| Hoeflea                 |
| Nitratireductor         |
| Phenylobacterium        |
| Rhizorhabdus            |
| Shinella                |
| Aminobacter             |
| Ochrobactrum            |


Taking into account all the genus collected we can start from the following non-redundant table with genus encomprassing rhizobia and non-rhizobia genus:

| Genus                | Genus                   | Genus            | Genus         |
| :------------------- | :---------------------- | :--------------- | :------------ |
| Agrobacterium        | Brevibacillus           | Mesorhizobium    | Rhizorhabdus  |
| Aminobacter          | Bosea                   | Methylobacterium | Rhodococcus   |
| Arthrobacter         | Burkholderia            | Micromonospora   | Shewanella    |
| Azospirillum         | Cupriavidus             | Microvirga       | Shinella      |
| Bacillus             | Devosia                 | Niastella        | Sinorhizobium |
| Bradyrhizobium       | Ensifer                 | Nitratireductor  | Solibacillus  |
| Paenibacillus        | Ohtaekwangia            | Nocardioides     | Streptococcus |
| Pantoea              | Phenylobacterium        | Ochrobactrum     | Streptomyces  |
| Phyllobacterium      | Pseudomonas             | Rhizobacter      | Tumebacillus  |
| Rhizobium            | Rhizobium/Agrobacterium | Halomonas        | Enterobacter  |
| Escherichia_Shigella | Hoeflea                 | Lysinibacillus   |               |



# State of the art: data available

How many accessory plasmids do we have/know for s. meliloti and related species?

Let's check:

1. Total number of plasmids are available for each specie of **Sinorhizobium**.
2. Total number of plasmids below 500kb for each specie of **Sinorhizobium**.
3. Total number of small, medium and large plasmids for each specie of **Sinorhizobium**.
4. Total number of plasmids below 500kb for each genus of **Rhizobiaceae**.
5. Total number of plasmids below 500kb for each species of **Rhizobiaceae**.

# Clustering accessory plasmids

For clustering accessory plasmids I used ***MGE-Cluster***. 

I am using 1,775 plasmids belonging to species classified in the core genus from the Alfalfa nodule reported in the study previously mentioned.

In this [notebook](https://webfs/n/projects/jp2992/MOLNG4331/code/plots_for_grant.ipynb) I made some plots to visualize *Sinorhizobium* plasmids inter and intra species


# The ambiguity hidden in the short reads assembly
 
 One of the reasons this project needs to invest in long read technology is that PsymA is not the only hotspot for horizontal gene transfer in *Ensifer* species,   accessory plasmids are also be part of the mobilome, exchanging genes between each other.

Here I would like to explore 2 plots:
1. Homology between accessory plasmids and PsymA
2. Pan-genome changes between core and accessory plasmids.



*Soil origin and plant genotype structure distinct microbiome compartments in the model legume Medicago truncatula*

*Population Genomics of the Facultatively Mutualistic Bacteria Sinorhizobium meliloti and S. medicae*



# References

The first step is to get literature, specially metagenomic studies, describing the bacterial diversity in the Rhizobiome of Medicago sp. (Alfafa). So we have a starting dataset.

[1] *Soil origin and plant genotype structure distinct microbiome compartments in the model legume Medicago truncatula* Try to answer 5 relevant questions:

1. To what extent do plant genotype and soil origin structure the microbiome?
2. Do plant compartments (rhizosphere, root endosphere, nodule endosphere, phyllosphere) harbor distinct microbiomes, and how are these affected by plant genotype and soil origin?
3. Are there specialist microbial taxa in the nodule, and how is this community assembled (i.e., from the rhizosphere or root endosphere)? 
4. Next we perform an additional inoculation experiment, adding one of four _Ensifer_ strains to ask: Does genetic variation in rhizobia influence the broader microbiome, and in what compartments?
5. Finally, we use additional shotgun metagenomic sequencing of a subset of root, nodule, and leaf samples to explore the genetic variation in _Ensifer_ bacteria throughout the plant.

[2] *Phage-plasmids promote recombination and emergence of phages and plasmids:* here is present an interesting methodology that can work for us. To evaluate the gene flow between P-P, phages and plasmids they recognized a classical phylogeny cannot be applied due to their high level of recombination and fast changing. 

[3] *Comparative analysis of integrative and conjugative mobile genetic elements in the genus Mesorhizobium*

[4] *Plasmid Flux in Escherichia coli ST131 Sublinhese methodology can be interesting for us. The limitation here is that *E. coli* does not present mega-plasmids, so we cannot use WGS as probably the graph will be a mess. Can it just used assembled genomes? 

[5] *Nodule Microbiome: N2-Fixing Rhizobia Do Not Alone* This review presents a description on the lesser-known bacteria that dwell within nitrogen-fixing nodules, although some of them are not N2-fixing organism they can enhance legume survival under stress conditions.  

[6] *Comparison of Nodule Endophyte Composition, Diversity and Gene Content Between Medicago Truncatula Genotypes* 

[7] *Cooperation, Competition, and Specialized Metabolism in a Simplified Root Nodule Microbiome*

[8] *Medicago root nodule microbiomes: insights into a complex ecosystem with potential candidates for plant growth promotion*