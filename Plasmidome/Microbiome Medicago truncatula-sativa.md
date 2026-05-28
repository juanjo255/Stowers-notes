
The idea here is to compile all the species that metagenomic studies has identified as part of the *Medicago truncatula* and *Medicago sativa* which are the legumes of interest for Sankari lab and

The plasmids from all species were retrieved from the PLSDB 2024v2 and we kept below 500Kb.



`PLSDB path: /n/projects/jp2992/MOLNG4331/biocomp_tools/plsdb `

# Final Dataset

The literature mining below compiled genuses found in the microbiota of *Medicago truncatula* and *Medicago sativa*, although the latter is less represented.

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
All the genuses are here `/home/jp2992/MOLNG4331/biocomp_tools/plsdb/stats_plsdb`

Because *M. truncatula's* microbiome is better reported, it is a good start to visualize plasmids relationships with *S. meloti* plasmids.


# Literature Mining


[Brown et al. (2020)](https://doi.org/10.1186/s40168-020-00915-9) presented the *core OTUs found within nodule communities across sampling design, an OTU was defined as core if present in >50% nodule samples*

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

> *Because Ensifer was the dominant taxon in all compartments, and MED analysis at the 16S rRNA gene indicated minimal diversity within Ensifer OTUs, we used metagenomic shotgun sequencing to further examine genome-wide similarity of Ensifer populations across different compartments. Ensifer scaffolds reconstructed from root endophyte and nodule communities had, on average, 99% global sequence identity in homologous regions—suggesting that Ensifer are extremely similar throughout an individual plant. Moreover, our estimate of the fraction of Ensifer cells containing each of the two symbiotic megaplasmids did not significantly differ between plant compartments (W = 132, P = 0.10 for pSMED01; W = 151, P = 0.14 for pSMED02; Fig. [4](https://link.springer.com/article/10.1186/s40168-020-00915-9#Fig4))—again suggesting that Ensifer are highly similar throughout the plant, including at the symbiosis megaplasmids.*

 ****
 
[Martínez-Hidalgo & Hirsch (2017)](https://doi.org/10.1094/PBIOMES-12-16-0019-RVW)focused on nonrhizobial bacteria usually found within nitrogen-fixing nodules. 

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

Additionally, they reported some bacteria non-nodulating found in nodules. I select only reported in Medicago: 

| Phylum                   | Bacterial genus |
| ------------------------ | --------------- |
| **Firmicutes**           | Paenibacillus   |
| **Actinobacteria**       | Micromonospora  |
| **Alpha-Proteobacteria** | Azospirillum    |

****

Similarly, other studies:
* *Cooperation, Competition, and Specialized Metabolism in a Simplified Root Nodule Microbiome*
* *Medicago root nodule microbiomes: insights into a complex ecosystem with potential candidates for plant growth promotion*

Presented accessory Families and Genus using 16S approaches in M. truncatula and M. sativa.


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


> [!warning]
> This is exploratory, it had more data than we needed. However, It helped to determined that, at a plasmid network level, *S. meliloti* actually presents a niche or limited interaction network.
>


# Some Plots with Public Data

How many accessory plasmids do we have/know for s. meliloti and related species?

Let's check:

1. Total number of plasmids are available for each specie of **Sinorhizobium**.
2. Total number of plasmids below 500kb for each specie of **Sinorhizobium**.
3. Total number of small, medium and large plasmids for each specie of **Sinorhizobium**.
4. Total number of plasmids below 500kb for each genus of **Rhizobiaceae**.
5. Total number of plasmids below 500kb for each species of **Rhizobiaceae**.
