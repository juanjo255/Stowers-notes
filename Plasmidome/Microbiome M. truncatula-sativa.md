
# State of the Art: Plasmid Database

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

Additionally, they reported some bacteria non-nodulating found in nodules. I select only reported in Medicago: 

| Phylum                   | Bacterial genus |
| ------------------------ | --------------- |
| **Firmicutes**           | Paenibacillus   |
| **Actinobacteria**       | Micromonospora  |
| **Alpha-Proteobacteria** | Azospirillum    |

similarly, other studies [6,7,8] presented accessory Families and Genus using 16S approaches in M. truncatula and M. sativa.

Taking into account the genus presented in the previous studies, we can start from the following non-redundant table with genus encompassing rhizobia and non-rhizobia genus:

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


> [!NOTE]
> This was exploratory, it had more data than we needed. However, It helped to determined that, at a plasmid network level, *S. meliloti* actually presents a niche or limited interaction network, that it is also reflected by the plasmid network.
>


# Some Plots with Public data

How many accessory plasmids do we have/know for s. meliloti and related species?

Let's check:

1. Total number of plasmids are available for each specie of **Sinorhizobium**.
2. Total number of plasmids below 500kb for each specie of **Sinorhizobium**.
3. Total number of small, medium and large plasmids for each specie of **Sinorhizobium**.
4. Total number of plasmids below 500kb for each genus of **Rhizobiaceae**.
5. Total number of plasmids below 500kb for each species of **Rhizobiaceae**.
