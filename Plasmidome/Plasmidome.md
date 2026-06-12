

# Objective

PsymA for years has been consider a biggest hotspot for intra-strain variability and accessory gene acquisition by horizontal gene transfer, however it has been found that S. meliloti can also carry accessory plasmids, plasmids that have been proven to also carry competence genes affecting symbiosis. 

During this project, we will collect all the accessory plasmids available for *S. meliloti* along with other assembled in-house and with collaborators, and make a description of the diversity of these plasmids in *Sinorhizobium meliloti*. 
 

```table-of-contents
```



# Data

We count we four sources of data:

1. PLSDB: 2024v2 was downloaded and filtered for only sequences below 500Kb.
2. In-house PacBio: [[Processing 48 Sinorhizobium meliloti Strains]]
3. PacBio from Penn State:[[Penn State Strains (Liana)]]
4. Nanopore from Dakota:[[Dakota Collab Assembly Report]]

# Results

## Whole Genome Sequencing (WGS)

We count we three WGS data: 
 1. In-house PacBio: [[Processing 48 Sinorhizobium meliloti Strains]]
 2. PacBio from Penn State:[[Penn State Strains (Liana)]]
 3. Nanopore from Dakota:[[Dakota Collab Assembly Report]]

Each document present each processing: Assembly, filtering and plasmid retrieval. In summary:

### Completeness 

I considered the Single-copy Orthologous maker genes searched by checkM, the number of contigs and the number of circular contigs.

![[compleness_all_datasets.png]]

So far there are no linear contigs reported for *Sinorhizobium meliloti*, therefore I expect most of the contigs to be circular, however, due to the low depth (check below) for some genomes, there is a high level of fragmentation especially of the mega-plasmids and putative accessory plasmids.

![[number_circular_contigs_per_dataset.png|685]]


### Contamination

| arker lineage            | Count | Note                                            |
| ------------------------ | ----- | ----------------------------------------------- |
| g__Ensifer (UID3566)     | 225   | -                                               |
| g__Pseudomonas (UID4526) | 1     | MAG154_2_filtered                               |
| o__Rhizobiales (UID3654) | 1     | m64404e_240531_162148.hifi_reads.bc2090--bc2090 |

### Length, GC and Depth Per Chromosome

![[len_QC_distri_all_datasets.png]]

[genome_qc.ipynb](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/code/genome_qc.ipynb)

Notice that for some genomes inside the Penn and Dakota datasets if I filtered base on 30x coverage based on my "Other" sequences which represent everything that could be an accessory plasmids, I would lose most of the data, however if I consider, for example, only the chromosome, I lose less than 25% of my data.

Some assemblies caught my curiosity. These have contigs with greater lengths than the mean. They were carrying chromosomes > 4Mb and some cases only presenting only 2 contigs > 1Mb (presumably pSymB is missing). 

For example, I investigate the assembly from **contig_2_P9E10_R3L_R4X** and it matches with *S. meliloti*, however it does not present pSymB. A mapping between the its assembly and a S. meliloti reference revealed that pSymB might be contained inside the Chromosome: [map_to_ref.html](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/dakota_collab_P9/flye_asm/P9E10_R3L_R4X/medaka_polish/map_to_ref.paf.html) 

The table Below the strains that were carrying a Chromosome > 4Mb with the number of contigs > 1Mb:

| sample_id                                           | # contigs > 1Mb |
| --------------------------------------------------- | --------------- |
| **P9E10_R3L_R4X**                                   | 2               |
| **P9F10_G8T_R4X**                                   | 2               |
| P9F12                                               | 3               |
| P9G1                                                | 3               |
| P9G10                                               | 3               |
| P9G11                                               | 3               |
| P9G12                                               | 3               |
| P9G9                                                | 3               |
| **m64404e_240423_150118.hifi_reads.bc2010--bc2010** | 2               |
| m64404e_240423_150118.hifi_reads.bc2013--bc2013     | 3               |
| m64404e_240423_150118.hifi_reads.bc2069--bc2069     | 3               |
| m64404e_240423_150118.hifi_reads.bc2077--bc2077     | 3               |
| m64404e_240423_150118.hifi_reads.bc2084--bc2084     | 3               |
| m64404e_240423_150118.hifi_reads.bc2090--bc2090     | 3               |
| m64404e_240531_162148.hifi_reads.bc2060--bc2060     | 3               |
| m64404e_240531_162148.hifi_reads.bc2074--bc2074     | 3               |
| **m64404e_240531_162148.hifi_reads.bc2076--bc2076** | 2               |
| m64404e_240531_162148.hifi_reads.bc2079--bc2079     | 3               |


> [!question]
> For strains with only two contigs: Is this an assembly error or the pSymB was actually "consumed"?
> Coverage metric looks good and it is circularized... 


### Strains Amino acid Identity (AAI)

To confirm their genetic identity, Mash tree was constructed using 3308 RefSeq genomes from the family _Rhizobiaceae_, which placed all our strains within the genus *Sinorhizobium*. Likewise, after Whole-Genome Similarity (ANI) estimation with fastANI all genomes achieved ANI greater than 99% with *Sinorhizobium meliloti*  genomes. thereby confirming their taxonomic position


![[tree_rhizobiaceae_w_our_strains.png|800]]



Whole-genome similarity ANI estimation via FastANI between the genomes in this study revealed that, as expected based on sample origin, the Penn State dataset (blue) showed the highest within-group similarity, followed by the Dakota dataset (red), while the in-house sequenced genomes (green) exhibited the greatest spread.

![[ANI_strains.png | 400]]

Further comparative identity analysis using strain Rm1021 as the reference revealed high proteome coverage (>78%) and average nucleotide identity (>98%) across all genomes. _Sinorhizobium meliloti_ is known to possess an open pan-genome, a characteristic that underpins its high genetic variability. This openness results in a vast repertoire of accessory genes, which have been suggested to support the extensive phenotypic diversity observed within the species [ref 1](https://doi.org/10.1186/1471-2164-12-235), [ref2](https://doi.org/10.1371/journal.pcbi.1004478). 

![[AAI_strains_to_ref.png|400]]


## Accessory Plasmids general description

### *De novo* Accessory Plasmid contigs identification

Considering the high level of genome fragmentation and the low database representation of *S. meliloti* accessory plasmids, in order to use as much data as possible, a de novo approach to identify accessory plasmids was considered. Sequence Bray-Curtis distances using 3-mer composition were computed with pdist from Scipy package, followed by a PCoA dimensional reduction KMeans Clustering algorithm from scikit-learn was used to establish clusters for further analysis. A similar approach was taken by [Wong, Finan & Golding (2002)](https://doi.org/10.1007/s10142-002-0068-0) when trying to discern the biology of the pSymB replicon and its relationship with the chromosome and megaplasmids using dinucleotide signatures.

![[trinucleotide_comp_contigs.png]]


We observed a clear separation among sequences classified as Chromosome, pSymA, pSymB, and Other—the latter encompassing fragmented sequences or accessory plasmids. Clusters 2, 3, and 0 corresponded clearly to Chromosome, pSymA, and pSymB, respectively. However, the remaining clusters did not consistently align with accessory plasmids. To further investigate, we examined the GC content and length distributions of these clusters using sequences greater than 10kb. The analysis suggested that only cluster 1 likely contains biologically relevant information, nonetheless, cluster 4 was retained in the analysis to account for the possible presence of small plasmids.

![[de_novo_len_gc.png|800]]


Code for plots: [assembly_kmer_clustering.ipynb](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/code/assembly_kmer_clustering.ipynb)

### Plasmid De-Replication

MobMess was used for containment-based de-replication. Due to the sequence similarity observed between the megaplasmids—particularly pSymA—and accessory plasmids, the megaplasmids were retained in the analysis to prevent false positives that could arise from fragmented sequences and lead to ambiguous plasmid assignments. Likewise, to identify new plasmid sequences collected during this study, _S. meliloti_ plasmids reported in PLSDB—along with related plasmids identified with mash clustering by MOB-typer—were retrieved using the keyword "_meliloti_".

MobMess is a tool for pan-genome study of plasmidome, it tries to identify *plasmids systems* by establishing containment relationships between plasmids. This strategy allows to handle complex scenario where we have to distinguish between fragments and complete plasmids while keeping as much data as possible. 

![[mobmess_all_plsdb.png | 800]]
[mobmess_network.html](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/plasmids_decontamination/mobmess_all_plsdb/mobmess_network.html)

After filtering *fragment* cluster (coloring top 20 clusters):
![[mobmess_clusters_filtfragments.png|453]]
![[mobmess_cluster_types_pre_post_filter.png]]
Using MobMess, we successfully de-replicated our accessory plasmids. The tool correctly identified points of fragmentation that resulted from sequence ambiguity between the accessory plasmids and mega-plasmids. For example, cluster 129 (red) corresponds to fragments between 12kb-15kb that causes assemblies ambiguities between pSymA (big points) and a group of accessory plasmids (small green points)

![[cluster129.png|145]]
 caption: size points correspond to sequences binary > 1MB (likely pSym). the color of the edge is the ANI (min. possible value is 90%) 


The following image presents what I call a simple in high level but complex on its details. which I think might help me track relevant genes been transferred across strains (this represent possible plasmid fusion, check plasmid fusion part).

![[simple_but_complex.png|210]]

We have two backbones (light green) connected by a compound cluster (dark green), and one of the backbones is uniquely connected to a maximal cluster (purple). The latter are connected to 3 different fragments cluster coming from the same assembly, that likely is the same plasmid, but it is fragmented due to a low assembly coverage (mean 10x). The compound cluster is a very interesting point of decision. Probably with other parameters using similarity clustering (check fastaANI below) these plasmids would be gathered together into the same cluster and probably same PTUs by COPLA (I could not install it nor even the database), however here we can see that only two plasmids create the connection between two different plasmid identities.

From MobMess output, as expected, I am interested in backbone, maximal and compound clusters, but in fragments cluster as well, since it will help me track distribution, i.e.  what the strains presents a type of plasmids. For example, the cluster in the image below shows a group of plasmids that due to low coverage were fragmented down to half of the closer backbone (light green). However, it can also represent a incomplete backbone.  

![[example_fragment_cluster.png|161]]

However, in maximal cluster all non-circular plasmids were filtered out to remove ambiguity. Unfortunately, this leads to the loss of some plasmid information, for example, 
*contig_5_m64404e_240531_162148.hifi_reads.bc2053--bc2053* and *contig_7_m64404e_240423_150118.hifi_reads.bc2055--bc2055* are two large plasmids that belongs to the same cluster, but its assembly is fragmented. See assembly below colored by depth. The next image shows the maximal cluster in the Mobmess network. All the elements connected are fragments below 20kb.

![[example_maximal_lost.png|200]]

![[example_maximal_lost_mobmess.png | 200]]

*P9C7* and *contig_11_m64404e_240423_150118.hifi_reads.bc2080--bc2080* carry each a unique plasmid which is lost as well.

![[example_P9C7_maximal_lost.png | 200]]
![[example_bc2080_maximal_lost.png | 200]]
> [!NOTE]
> The decision of removing non-circular in maximal comes from cases like *contig_3_P9H2* and *contig_9_P9E8*. They look like the assembly above, where there is a sequennce of a considerable size (in this case 50kb) connected to a small sequences (this case 3kb) and the latter connected to a mega-plasmid. Except that in this case it looks more like an ambiguity cause by a IS.

From this, I can conclude that MobMess output can help me answer two questions: What is the diversity (backbone and compound)? and What is the distribution (backbone, compound and fragmented)? 

> [!QUESTION]
> Can we establish a computational methodology to handle this problem? Cause the assembly is evidently saying that there is two paths in the assembly. The plasmids is actually near complete. Some alternatives come to my mind:
> 1.  *node2vec* This tool converts nodes into vectors considering neighboring connections.
> 2. *Simple script to determine the nature of the ambiguity using the GFA*: I have noticed that so far the ambiguities of real acc. plasmids are with sequences around 10kb, higher than IS. Also, the coverage is lower than the mega-plasmid. 
> 

### ANI vs AF de-replicated plasmids

The following kdeplots were plotted using the maximum plasmid length (plot 1) and using the minimum plasmid length for each pair. Considering these are big plasmids with sizes between 50-700kb, plot 1 shows a dense cluster in AF ~0.3-0.4, and the distribution extends much more toward high ANI + high AF in the upper right corner, representing Plasmids nearly identical and one contained in the other (i.e fusions). On the other hand, the plot 2 shows the dense cluster sits at high ANI (~85-90%) but very low AF (~0.2), meaning large plasmids have a lot of unique sequence and they are likely to share large plasmids sharing a small conserved region. This hinders plasmid clustering using classical approaches such as COPLA, as it would mask selective ecological pressures that may have shaped these large plasmids, while also potentially overestimating horizontal gene transfer events within a group of plasmids.

**Plot 1**
![[plot2_kdeplot_ani_vs_af.png|300]]
**Plot 2**
![[plot1_kdeplot_ani_vs_af.png|300]]

[uniq_pls_ANI.ipynb](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/code/uniq_pls_ANI.ipynb)
### Plasmid Diversity in *Sinorhizobium meliloti* 

To measure plasmid diversity in the dataset, we determine unique plasmid identities from the MobMess output by considering three categories: backbone plasmids (complete plasmids), compound plasmids (the maximal size of a plasmid system), and maximal clusters where all members are below 1 Mb and present at least one sequence circular.

We retrieved 33, 125, and 171 accessory plasmids from the _in house_, _Dakota Nanopore_, and _Penn State_ datasets, respectively, totaling 346 plasmids out of the initial 532 sequences. After de-replication using MobMess, we obtained 28, 51, and 9 unique plasmid clusters from each dataset, respectively. Notably, very few plasmids were shared across datasets, suggesting ecological specificity. Interestingly, the Penn State dataset contained the highest number of total sequences but yielded the lowest number of unique plasmids, consistent with their isolation methods. **The initial, 532 putative plasmids sequence retrieved from the 256 genomes sequenced was reduced to 304 unique accessory plasmids, and 223 are new plasmids sequences reported in this study.** No linear plasmid, as described by [Hawkey et . al (2022)](https://doi.org/10.1099/mgen.0.000807), was found in these strains.


| Dataset composition                     | compound | maximal | backbone | Total Clusters | Total Seqs |
| --------------------------------------- | -------- | ------- | -------- | -------------- | ---------- |
| [database]                              | 6        | 0       | 2        | 8              | 17         |
| [penn_state]                            | 4        | 2       | 3        | 9              | 134        |
| [dakota_nanopore]                       | 3        | 42      | 6        | 51             | 120        |
| [in_house]                              | 3        | 24      | 1        | 28             | 33         |
| [dakota_nanopore, penn_state]           | 0        | 1       | 0        | 2              | 0          |
| [database, in_house, dakota_nanopore]   | 0        | 1       | 0        | 1              | 0          |
| [database, penn_state, dakota_nanopore] | 0        | 0       | 3        | 3              | 0          |
| **Total clusters**                      | **16**   | **70**  | **15**   | **101**        | -          |
| **Total seqs**                          | **31**   | **113** | **159**  | -              | **303**    |



For further analysis, **database plasmids were kept only if it is a backbone or compound cluster**. This because I extracted the plasmids related with S. meliloti, that is plasmids that where close to S. meliloti according to MOB-typer typing file from the PLSDB. Therefore, it contains plasmids that is not reported in the S. meliloti. **However, database plasmids will be consider during gene repertoire relatedness network creation**.

Nonetheless, considering that plasmids due to its high variability we inspect the gene content relatedness among these plasmids, and if these plasmids could be cluster into higher categories representing biological features shared among them.


### Plasmid Clustering

Plasmid classification is challenging due to high rates of genetic gain and loss, which drive plasmid divergence. To address this, different tools have been developed to classify plasmids into discrete groups. For example, among the two most popular scheme for plasmid classification are PlasmidFinder and MOB-Suite. The former is based on replicon types [Carattoli et. al (2005)](https://doi.org/10.1016/j.mimet.2005.03.018) while the latter relies on mobility (MOB) groups [Garcillán-Barcia et. al (2009)](https://doi.org/10.1111/j.1574-6976.2009.00168.x). However, they are limited to a number of taxonomic groups, especially, the replicon typing by PlasmidFinder is dependent of experimental evidence, making it impractical for organism with poor sequencing representation or lack experimental data. Additionally, these schemes poorly reflect plasmids genetic relatedness. COPLA, a network-based approach for plasmid classification, introduced the term of Plasmid Taxonomic Unit (PTUs)  [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2), but this is intended to cluster widely across bacterial species, losing species resolution. Additionally, COPLA is not maintained software and its installation, including its database needed for PTUs classification, was not possible. Nonetheless, Network-based alternatives to study plasmidome has been proposed [Shapiro et. al](https://doi.org/10.1038/s41396-023-01373-5) [Arredondo-Alonso et. al](https://doi.org/10.1038/s41467-025-57940-1) [Lipworth et. al](https://doi.org/10.1038/s41467-024-45761-7) [Matlock et. al](https://doi.org/10.1038/s41396-021-00926-w) [Fiamenghi et. al](https://doi.org/10.1038/s41467-025-65102-6) [Acman et al (2020)](https://doi.org/10.1038/s41467-020-16282-w) [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25). Considering the lack of agreement for plasmid clustering and our interest in describing the diverse functional capacities of accessory plasmids, **we decided to perform a function-based clustering. To accomplish this we cluster plasmids based on gene content**.  For this we used a genetic repertoire relatedness metric proposed by [Pfeifer et. al (2021)](https://doi.org/10.1093/nar/gkab064) which at the same time allow us to explore the horizontal gene transfer events. 





> [!NOTE]
> FastANI looks like a good approach, but given that clustering these large plasmids is a challenge as they might represent the fusion of smaller plasmids, I want to create a containment network where distances can give me evolutionary relations between plasmids. I found MobMess, it is a super interesting tool proposal that applies this approach and establish plasmids systems discerning between plasmids backbone genes and cargo genes. These two categories combine to form different plasmids structures. 
> 
> The other aspect to consider is the clustering algorithm. Louvain is popular algorithm for community discovery, however, it has been described that it can produce internally disconnected communities. An alternative was proposed called the Leiden algorithm.
> 
> Next it is a comparison between: in the left, Vclust + Leiden (resolution=1), and in the right, FastANI + Louvain (resolution=1). In this case Louvain and Leiden produce similar result. I used louvain since it is easier to run in python. they are both using tANI to filter >0.9 however I am plotting every edge with AF>0.7. **Only 10 clusters are colored.**
> ![[fastANI_vs_Vclust.png]]
> 
> We can see that FastANI might be overestimating the ANI. **Vclust + leiden can replicate MobMess, yet the latter provide extra relationship information**.
> 

 

****


The image below is an example of a systematic problem that shares several genomes from Penn State. This is an ambiguity that can easily confused since it can represent different scenarios in the genome assembly. However, we know it is an accessory plasmid, confirmed by plasmid features, kmer composition and re-sequenced of two of the samples (*Liana_052_1_filtered* & *Liana_056_3_filtered*). Additionally, it systematically has a coverage inferior to the chromosome and the symbiotic plasmids. This makes me think about a thought I had before with these large plasmids; low-copy number plasmids that restricted even in the same population, considering this data belong to same isolates, so either cells started losing them or the plasmid are restricted to subpopulations, vertical domination over horizontal to preserved plasmid diversity has been studied [Sabnis et. al](https://doi.org/10.1016/j.celrep.2025.116456)

With *S. meliloti* something curious happen, their plasmids are very large > 50kb up to 700kb, even more interesting during sequencing of isolates, *contig_4_m64404e_240531_162148.hifi_reads.bc2049--bc2049*  is an accessory plasmids of ~350kb and all the strains carrying the same plasmid presents a reduction in coverage (around halve total, check image below colored by depth), however *Liana_052_1_filtered* & *Liana_056_3_filtered* which were part of the re-sequenced strains are very similar and presents coverage as high as chromosome. Additionally, they presented another plasmid of 75kb.

![[example_ambiguity_w_acc_pls.png | 200]]



> [!NOTE]
> I am trying Vclust and MobMess!: Vclust allows me to achieve similar result as the pipeline used in this [soil plasmidome study](https://doi.org/10.1038/s41467-025-65102-6) . whereas MobMess is an interesting proposal that uses containment network to establish what they call "plasmids systems"
> 
> Vclust results are very clustering algorithm dependent. I tried all of them, and Leiden and complete linkage are my favorite. 


### Size and GC content distribution


![[len_QC_distri_all_datasets_plasmids.png | 400 ]]

After MobMess clustering, QC values were 48–65%, and plasmid sizes ranged from 12 kb to 700 kb. The 700-kb plasmids exceed the typical threshold for megaplasmids (~300 kb) and are unusually large for accessory elements. Notably, there are two assemblies containing this large plasmid, one of them presented the chromosome, pSymA, pSymB, and the accessory plasmid itself all circularized, however the other one was recognized as a Type I error. This observation is intriguing and may indicate that this replicon represents a mobilizable megaplasmid, or a recently "evolved" element.

>**Assembly graph with 700kb plasmid**
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9G4/assembly_graph.gfa

>**Assembly graph with False positive**
>/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/flye_asm/m64404e_240531_162148.hifi_reads.bc2049--bc2049/assembly_graph.gfa

![[len_GC_uniq_pls_mobmess.png | 500]]

![[len_GC_uniq_pls_kdeplotpng.png]]


### MOB, MPF and RepABC annotation

Our analysis revealed that accessory plasmids in our datasets harbored either MOBP or MOBQ. Interestingly, some plasmids contained both MOB proteins, a rare occurrence for accessory elements. While this initially suggested a possible Type I error (i.e., fragmented sequences from the complete pSymA, which encodes both MOBP and MOBQ), assembly graph inspection confirmed one ~400 kb plasmid with both MOBP and MOBQ as a genuine accessory element, with the pSyms and this plasmid all showing correct assembly and good coverage. A similar case  occurred with a sequence predicted with three MOB proteins (*MOBP,MOBQ,MOBQ*). The assembly graph inspection confirmed It belongs to a ~240kb circular plasmid with a coverage of 240x.


>Assembly graph with 400kb plasmid
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9C10/assembly_graph.gfa

> Assembly graph with 240kb plasmid
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9E7_R3L_R4X_Y9Q/assembly_graph.gfa


> [!QUESTION]
> Can this be a transitioning plasmid?? like an intermedia evolutionary state between an accessory plasmid and a mega-plasmid. two plasmids merged??
> 

> [!NOTE]
> By the way, in the same genome I saw a piece of around 1.5kb with high coverage (~50x), I think it might be a virus. An interesting example of a genome sequenced when a virus activated. 


![[mob_typing_uniq_pls_mobmess.png | 800]]

MOBQ/P was the most frequent relaxase, consistent with previous reports in Rhizobiaceae [Redondo-Salvo et. al (2020)]( https://doi.org/10.1038/s41467-020-17278-2). Outliers were identified based on size (<20 kb or >400 kb) and GC content (<50% or >62%). Inspection revealed: (i) a 13.5 kb _E. coli_ plasmid (48% GC); (ii) a 749 kb _S. meliloti_ plasmid (58% GC)—the largest non-pSym plasmid reported in this species; and (iii) a group of 12–23 kb sequences (64.8–65.8% GC) lacking relaxases and replication/partition systems, containing only biosynthetic gene clusters and hypothetical proteins. The latter group was present in the Penn State and Dakota datasets and it was excluded from further analysis. 

Nonetheless, notice that several plasmids were not annotated for a relaxase. Additionally, after gene annotation, a few plasmids did not present a RepABC and, a few, a relaxase neither. So, we decided to further inspect those sequences.

#### No RepABC

13 sequences did not presented an explicit repABC operon. Some of these plasmids seems to be very unique. They are annotated with proteins with alike domains, for example, in **contig_5_MAG342_3_filtered** "*ParB/RepB/Spo0J family partition protein*", "*ParA protein, putative plasmid partitioning protein*". 11 of them presented related annotations. The following file presents the related annotations: [repabc_like_hits_in_no_repabc.tsv](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/plasmids_decontamination/mobmess_all_plsdb/repabc_like_hits_in_no_repabc.tsv) 

Only **contig_12_P9E8** and **contig_1_m64404e_240531_162148.hifi_reads.bc2080--bc2080** lacked any associated annotation.

**Contig_12_P9E8** appears to be a plasmid related to a 9 kb suicide plasmid (MN057686.1) in _E. coli_. Another sequence, **contig_19_P9D4**, is a highly similar 9 kb plasmid. Due to this ambiguity, both were removed from downstream analysis.

In contrast, **contig_1_m64404e_240531_162148.hifi_reads.bc2080--bc2080** is a low-quality 129 kb plasmid. Nevertheless, it belongs to a group of complete circular plasmids that did contain a RepABC operon and a MOB protein.

Next table and plots shows the final counts:


| relaxase_type(s) | Count   | Notes           |
| ---------------- | ------- | --------------- |
| MOBQ             | 119     |                 |
| MOBP             | 87      |                 |
| -                | 68      |                 |
| MOBQ,MOBQ        | 25      |                 |
| MOBP,MOBP        | 3       |                 |
| MOBP,MOBQ        | 1       | ~400kb circular |
| MOBP,MOBQ,MOBQ   | 1       | ~240kb circular |
| **Total**        | **304** |                 |

| mpf_type  | count   |
| --------- | ------- |
| MPF_T     | 219     |
| -         | 85      |
| **Total** | **304** |

![[len_GC_uniq_pls_mobmess_filt.png|700]]
![[pls_features_stackbar.png]]
#### Replicon groups (Rh groups)

PlasmidFinder has been the plasmids classification gold standard by clustering plasmids into incompatibility groups. The incompatibility comes from plasmids that shares the same replication and/or partition system which makes compete in the same cell and therefore incompatible [del Solar et. al (1998)](https://www.ncbi.nlm.nih.gov/pubmed/9618448) . The incompatibility groups in plasmidFinder has been extensively established for plasmids in the order *Enterobacterales* [Orlek A. et al. (2023)](https://doi.org/10.1016/j.plasmid.2023.102684) In soil *α-Proteobacteria* such as _Sinorhizobium meliloti_, plasmid replication and partition are dominated by the repABC family, which is largely absent from Enterobacteriaceae and has not been integrated into the canonical Inc scheme ([Cevallos et al. 2008](https://doi.org/10.1016/j.plasmid.2013.08.001); Pinto et al. 2012).  

Of the 303 retrieved plasmids, 289 carried at least one *repA* and 284 of these contained a complete *repABC* operon. Only 1 plasmid (contig_4_P9F11) presented a *RepA* duplication, reason why it was remove from this analysis. Following the replicon typing schemes from previous studies [Cavassim et. al (2020)](https://doi.org/10.1099/mgen.0.000351)[Gorbitz et. al (2025)](https://journals.asm.org/doi/10.1128/mbio.02497-25#data-availability) *repA* was extracted for each plasmid and clustered using MMseqs2 with thresholds of >70% coverage and >90% identity. The *Rhizobium leguminosarum* replicon representative sequences were extracted from [Gorbitz et. al (2025)](https://journals.asm.org/doi/10.1128/mbio.02497-25#data-availability). Plasmids that did not cluster in any of Rh groups where annotated as Si[01-n] in order of decreasing abundance in the genome set.

We found that 36 and 52 plasmid sequences belonged to the Rh07 and Rh08 replicon groups, respectively, indicating plasmid transmission between *Rhizobium* and *Sinorhizobium*. The remaining 205 plasmid sequences, together with plasmids retrieved from PLSDB annotated for *Sinorhizobium meliloti*, formed 15 groups (designated Si01–15).

![[replicon_groups.png| 800]]
Based on this classification scheme, we further explored the Replicon group composition of the different strains. We observed that


![[repl_group_each_strain_heatmap.png]]

[replicon_groups.ipynb](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/code/replicon_groups.ipynb) 


##### Origin of Replication (oriV)

During a [[Comparison of Origin of Replication]] between the 44 strains assembled in house, we observed that the predicted oriV by PlasAnn presented different k-mer composition between accessory plasmids, pSymA, pSymB and the chromosome. Origin of replication were annotated for 225 out of 304 putative accessory plasmids sequences. The discrepancy between the amount of predicted oriV and RepABC might be because it depends on finding a RepA and matching an intergenic Spacer (IGS) sequence in proximity to the RepA hit.

Following annotation, we wanted to inspect the use of oriV as accessory plasmids identification. PCA from 6-mer composition of the oriV revealed a higher diversity in oriV oligomer composition among accessory plasmids compared to the pSymA, pSymB and Chromosome which showed a more conserved composition. 

pSymA, pSymB and Chromosome were extracted only from the *in house* dataset. pSymA and pSymB were annotated with PlasAnn, and the Chromosome with BAKTA. So far, this sample can be a good representative dataset since it shows the higher diversity according to the the  [[#Strains Amino acid Identity (AAI)]] analysis, other two dataset possibly due to the isolation experiments might present more related strains.

![[PCA_6mer_ori.png|400]]


However, once again the oriV is highlighted as an interesting feature to analyze for accessory plasmid sample purity. Inspecting the previous graph looking for *contig_7_m64404e_240531_162148.hifi_reads.bc2049--bc2049* a 700kb contamination described during [[#MOB and MPF typing]], we can noticed it was placed with pSymA group, its most probably source of origin. 

![[PCA_6mer_ori_cont_highligth.png | 400]]

## Gene Content Shared Between Accessory Plasmids And Main Replicons

We investigated the gene content sharing between accessory plasmids and the main replicons. In *Sinorhizobium meliloti* has been described as a specie with high gene content redundancy. [diCenzo & Finan (2015)](https://doi.org/10.1007/s00438-015-0998-6) were abled to reduce the genome size by 45% through the removal of the megaplasmids. However, it has been reported even if proteins seems to have a similar molecular function according to the amino acid similarity, they can perform unique biological role that do not complement, such as the case of the five Cu+-ATPases [Patel et al. (2014)](https://doi.org/10.1099/mic.0.079137-0). Therefore, to do the comparison we built a pan-genome with PPanGGoLin keeping the default values of 80% for coverage and identity. Also, we only consider genomes presenting circular chromosome and the megaplasmids according to Flye. Therefore, retrieved accessory plasmids were filtered accordingly. At end we counted with 172 genomes and 204 accessory plasmids.

We can see that pSymB shares more genes with the chromosome, whereas pSymA shares more genes with the accessory plasmids, reflecting their evolutionary differences where megaplamid pSymB reach a status of chromid and the megaplasmid pSymA keeps more  plasmid-like features. Interestingly, the chromosome shares more genes with the accessory plasmids than the pSymA.

![[gene_share_pls_and_chromosomes.png|400]]
![[gene_sharing_upset.png]]

[gene_redundacy.ipynb](/n/projects/jp2992/Plasmidome_project_MOLNG_4509/code/gene_redundacy.ipynb)

### To DO

Described the most common genes shared with the main replicons




## Accessory plasmids Present Diverse But Not Abundant Toxin-Antitoxin (TA) systems

Sinorhizobium meliloti accessory plasmids have been referred as *cryptic plasmids*, suggesting [Mercado-Blanco & Toro (1996)](https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf) [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411)  that their stability in the host bacteria could be due to mechanism which involves multimer resolution, active partition system and plasmid addiction or Toxin-Antitoxin (TA) system that ensures the vertical transmission by producing dependence. [Effe *et al.* (2025)](https://doi.org/10.1038/s41467-025-62473-8) investigate the evolutionary advantage provided by the combination of different persistent strategies that can be found in plasmids. The researches found that an active partition system coupled with a TA system provides the greatest fitness advantage, specially for low-copy extrachromosomal elements. This is specially relevant for *Sinorhizobium meloti*, since given the plasmid sizes distributions and high detection of the whole replication module ([[#Size and GC content distribution]]) suggesting that these large plasmids also relies on an active partition system to ensure their survival in the host bacteria as it has been suggested in other studies [Effe *et al.* (2025)](https://doi.org/10.1038/s41467-025-62473-8).  

![[TA_type_vs_length.png|800]]


![[heatmap_TA_systems_clustered.png|600]]
![[heatmap_TA_systems_mean_clustered.png|600]]

Thus, to annotate TA systems, the HMM models from TASmania were used. Currently there are two ways to annotate TA systems, using the highly curated TADB or using the more "discovery-oriented. TASmania presents higher sensitivity than TADB, however, TASmania  models were built mining for interpro annotated TA in more than 41k assemblies, therefore it has a higher risk of false positive. [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) annotated TA systems for approximately 10k plasmids using TASmania models, and they subsequently trained a Random Forest model which achieved 95% accuracy predicting PTUs. 

However, TASmania models due to its discovery approach and the difficulty to assess the its predictions, it is likely to produce a high false positive rate [Akarsu et al. (2019)](https://doi.org/10.1371/journal.pcbi.1006946) . Interestingly,  [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) reported that ParB/RepB/Spo0J, Hok/Gef, RelE/ParE, and PemI coding sequences were found among the most influential features for the model accuracy. Our plasmids replicated the same effect to that reported by [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) analysis, where there is a decreasing in the accumulation of TA systems along plasmids sizes. [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) suggested that larger plasmids can increase competence by presenting more beneficial accessory genes compared to small plasmids, therefore larger plasmids tends to reach a saturation point where TA systems offer little advantage and this can be overcome with the inclusion of other beneficial genes through HGT. Such effect has been observed in the context of Restriction-Modification (R-M) systems, [Shaw *et al.* (2023)](https://doi.org/10.1093/nar/gkad452) found that the escape from type II R-M system was associated with plasmid size and host range, implying that while small plasmids might adapt by small mutations, large plasmids opted to add additional beneficial genes providing higher vertical transmission at the cost of horizontal transfer.

RepB represented the most common partitioning protein among our plasmids dataset, and it was the most common annotation associated to TA model. Therefore, Rep annotation here might be related to the fact that TA systems have been found close to the RepABC operon broadly across *Rhizobiaceae* [Yamamoto et al. (2009)](https://doi.org/10.1128/jb.00124-09) [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411). Curiously, we observed cases with multiple annotations of partition-related proteins. While functional variability has been reported in the proteins of the RepABC **—** for example, [Ingmer & Cohen (1993)](https://doi.org/10.1128/jb.175.24.7834-7841.1993) demonstrated that RepA can be involved both in plasmid replication and partitioning **—** the conserved operon structure makes very unlikely to arise from a duplication and more probably indicates acquisition through plasmids fusion or cointegrate events [Hall et al. (2022)](https://doi.org/10.1098/rstb.2020.0472) [Qu et al. (2019)](https://doi.org/10.2147/IDR.S189168) [Wang et al. (2021)](https://doi.org/10.3389/fmicb.2021.754931). In deed, we found some clear signals of plasmids fusions events in our dataset which will be more explored below.

Notably, the second most common TA system corresponds to the ArdC protein, an anti-restriction protein of type C. _In vitro_ experiments by [Belogurov et al. (2000)](https://doi.org/10.1006/jmbi.1999.3493) demonstrated that ArdC can protect single-stranded DNA against the type II restriction endonuclease HhaI. Consequently, ArdC has been proposed to protect plasmids from host restriction-modification (R-M) systems during conjugation [Belogurov et al. (2000)](https://doi.org/10.1006/jmbi.1999.3493); [González-Montes et al. (2020)](https://doi.org/10.1371/journal.pgen.1008750).

While _Sinorhizobium_ species were initially thought to lack an R-M system [Capela et al. (2001)](https://doi.org/10.1073/pnas.161294398), subsequent plasmid electroporation experiments in _S. meliloti_ Rm1021 revealed increased transformation efficiency with non-self DNA in _hsdR_ mutants—a restriction enzyme belonging to a type I R-M system [Ferri et al. (2010)](https://doi.org/10.1016/j.plasmid.2010.01.001); [Dohlemann et al. (2016)](https://doi.org/10.1016/j.jbiotec.2016.06.033). In contrast, we did not find the most common bacterial R-M system (type II) in our strains. Given the host-restricted nature of _Rhizobiaceae_ plasmids, this observation amplifies the role of methylation systems in _S. meliloti_, as explored in other studies [diCenzo et al. (2022)](https://doi.org/10.1128/mSystems.01092-21); [Passeri et al. (2025)](https://doi.org/10.1093/gbe/evae245).

Together, this adds a layer of complexity to plasmid interactions between donor and recipient hosts. It has been suggested that plasmid conjugative transfer in _Rhizobiaceae_ is restrained by a combination of regulatory elements [Brom et al. (2014)](https://doi.org/10.1007/978-1-4614-9203-0_3); [Castellani et al. (2026)](https://doi.org/10.1128/spectrum.03242-25), and methylation patterns appear to be part of this regulatory framework [Dohlemann et al. (2016)](https://doi.org/10.1016/j.jbiotec.2016.06.033); [Passeri et al. (2025)](https://doi.org/10.1093/gbe/evae245).


Type II toxin-Antitoxin VapC system and the transcriptional regulator CopG were as well among the most common. Interestingly, the latter was recently identified as an important actor in the symbiosis of *Bradyrhizobium* sp. SUTN9-2 with legumes [Wangthaisong et al. (2024)](https://doi.org/10.3390/biology13060415) as well as an actor in the copy number control of conjugative plasmids  [Ni *et al.* (2021)](https://doi.org/10.1073/pnas.2011577118) 


> [!question]
> I**s TA systems related with genospecies?** look at this heatmap. they are colored by mobmess cluster, that it is expected to be together, however see how are some groups with more TA than others.
> ![[is_TA_corr_w_genoespecie.png|200]]
>
> 



## Gene Content Profiles Indicates Different Ecological Pressures between Accessory Plasmids

Large accessory plasmid are thought to provide fitness improvement in complex ecological environments such as in the soil microbiome  [Hall et al. (2022)](https://doi.org/10.1098/rstb.2020.0472), and particularly for *Sinorhizobium meliloti*, it has been proposed that accessory plasmids might provide advantages over no accessory plasmids strains carrier [Schuleter et. al (2007)](https://doi.org/10.1111/j.1574-6968.2007.00731.x). During a long-term field release experiments [Selbitschka et al. (2006)](https://doi.org/10.1007/s00248-006-9056-6)observed that *S. meliloti strain SM11* out-competed genetically modified *S. meliloti strain 2011*. Therefore, we wonder if plasmids could present differences in gene content that might indicate plasmid response to specific sites of isolation.

To further investigate the biological differences between these accessory plasmids, we used EggNOG-mapper to assign Clusters of Orthologous Genes (COGs), and a COG frequency matrix was computed and normalized by number of genes, finally a distance matrix was calculated using Bray-Curtis and plotted in PCoA. 

We found that gene functions in plasmids are not limited to the dataset of origin (right) let alone the replicon group (left), where we can see overlapping between plasmids from different dataset, and replicon type presenting a closer gene functions relation to different replicon groups. This is consistent with other studies that have suggested that classification of plasmids by replicon or MOB types have poor resolution and does not capture information about the gene content of plasmids [Douarre et. al (2020)](https://doi.org/10.3389/fmicb.2020.00483) [Orlek at. al (2017)](https://doi.org/10.3389/fmicb.2017.00182) [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2).  After clustering with HDBSCAN and using Fisher Exact Test with BH correction, we found only differences between Defense mechanism, Nucleotide transport and metabolism, and Cell mobility. 

![[COGs_feq_matrix_pcoa.png]]

![[COG_enrich_unq_pls.png]]

![[COG_plasmids.png]]

Nonetheless, we observed that there are cluster of plasmids presenting endemic gene composition, particularly true in the case of Penn State dataset. Due to the poor gene functional description of these plasmids, they carry a high number of hypothetical proteins, which hinders the significance of the COGs, therefore we replicated this analysis but using the pan-genome of all plasmids. We compute the pan-genome of the plasmids using Panaroo. Panaroo uses context and a lower clustering threshold (70%) to combine diverse gene families into a single gene. Because of the high rates of genetic rearrangement and divergence among plasmids, we apply a more flexible threshold during the initial protein clustering, yet keeping a plasmid species metric level (90% id. and cov.). Pan-genome construction was followed by dissimilarity matrices calculation using *pdist* from *Scipy* python package and plotted in a MultiDimensional Scaling (MDS).

![[gene_content_pls_MDS_panaroo.png | 800 ]]

MDS analysis yielded three main insights. First, plasmid clustering is not determined to individual datasets, as some overlap between datasets was observed. Second, clear differences exist among plasmids from the same dataset—most notably within the Penn State dataset. Third, the stress value of 0.36 indicates that two-dimensional space is insufficient to accurately represent plasmid distance relationships.


## Mobile Genetic Elements Cointegrate Promote Megaplasmid Formation in _Sinorhizobium meliloti_

Plasmids carrying antibiotic resistance genes have been reported harboring multiple replicons, and MGE-mediated plasmids fusions have been proposed as one important mechanism for plasmids diversity, protecting against plasmids incompatibility, enabling cross-host transfer of non-conjugative plasmids and even amplifying antimicrobial resistance by creating multidrug resistant megaplasmids [Wang et al. (2021)](https://doi.org/10.3389/fmicb.2021.754931) [Liu et al. (2025)](https://doi.org/10.1093/jac/dkaf309) [Ipoutcha et al. (2026)](https://doi.org/10.64898/2026.01.09.696371) 

Plasmids fusions represents a point of plasmid evolution that support the rapid emergence and persistence of multidrug-resistant plasmids across bacterial pathogens [Wang et al. (2021)](https://doi.org/10.3389/fmicb.2021.754931). In a recently published study [Penadez et. al (2026)](https://doi.org/10.64898/2026.01.09.696371), researches observed that under antibiotic pressures plasmids fusion mediated by MGE was promoted. *Sinorhizobium meliloti* genomes in this study presents a right skewed towards large plasmids with sizes > ~60kb. Studies on plasmidome description along the prokaryote kingdom  [de la cruz et al. (2010)](https://doi.org/10.1128/mmbr.00020-10) and in specific largely sequenced bacterial species [cite](), has reported that plasmids sizes shows a bimodal distributions attributed to the difference between small and large plasmids, or non-mobilizable and conjugative plasmids. As we observed most of the plasmids recovered here presented a relaxase and a mate pair formation (MPF) system.

Therefore, we investigate the number of Rep proteins in each plasmids. Interestingly, most of the plasmids harbors multiple copy of proteins of the RepABC module, indicating possible plasmids fusion events. The following plots are sorted by length colored by the product in annotations. The plots show the same. PlasAnn is preferred as they attempted to reduce annotation redundancy that we can notice in BAKTA.
![[num_repABC_per_pls_plasAnn.png]]
![[num_repABC_per_pls.png]]

 Using MobMess, we can observed several such events. For example, *contig_4_m64404e_240531_162148.hifi_reads.bc2042--bc2042* is a ~314kb plasmid product of the fusion of two plasmids (~158kb and ~146kb) mediated by transposases from the Tn3 family. [Check protein alignment >90% of three representatives](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/plasmids_decontamination/2_contained_in_one.html). Similarly, *contig_3_m64404e_240423_150118.hifi_reads.bc2012--bc2012* represent a ~149kb plasmid that contains a 73kb plasmids flanked also by a Tn3 transposase family [Check protein alignment >90% of three representatives](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/plasmids_decontamination/contig_4_bc295_vs_contig_13_bc2012.html) 

**Image below shows both plasmids cointegrates**: plasmid fusion, and plasmid and MGE cointegrate (possibly an ICE).

![[inset_image_pls_fusion.png|531]]

Indeed, Tn3-family transposons belong to class 2 transposons which along with the Tn7-family and are a class of complex transposition elements associated with a high influence in the generation of co-integrates between plasmids and other MGEs [Szuplewska et al. (2014)](https://doi.org/10.1080/2159256X.2014.998537) This observations lead us to ask if accessory plasmids were presenting IS composition differences which might involve in the gene exchange between accessory plasmids. 

We found that accessory plasmids indeed seems to have specific enrich of certain IS families. 


|                                   |                               |
| --------------------------------- | ----------------------------- |
| ![[IS_comp_per_cluster.png\|400]] | ![[IS_comp_per_pls.png\|400]] |
|                                   |                               |



### Curiosity in pSymA

I have noticed that it is possible that the important genes for plasmid backbone can accumulate close to the replication proteins. Revision in some pSymA with more than one Rep I see that it is common to find TA system and ABC transporters. 

I extracted those regions and aligned them with clinker [pSymA.html](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/pSyms_fusions_backbones/pSymA.html)

I have not concluded nothing this is curiosity to see if we can map plasmids fusions in this replicon and others.

#### TO DO

Check this on chromosome and psym in each strain might be interesting to see if there is sharing of transposition elements. I would like to think of these plasmids a sponges 

## Accessory Plasmids Present Unique Genomic Arrangements Possibly  Indicating Specialized Ecological Pressures

To determine whether the unique accessory plasmid clusters exhibit specific proteins or structural variations that characterize their ecological niche—or confer traits that enhance survival in their host—we leveraged the pan-genome of the plasmidome built with Panaroo. Panaroo, in addition to protein families, reports structural variations based on annotating triplets for each sample as long as min_edge_support_sv is support (3), subsequently, we cluster plasmids using HDBSCAN using a precomputed jaccard distance matrix, then we used a simple linear model followed by Fisher Exact Test and BH correction. This approach allowed us to identify important structural  that could possess distinct functional features relevant for the symbiosis under specific ecological pressures.

![[SV_MDS_uniq_pls.png]]

We can recover several gene organization related with transcriptional regulators, and membrane proteins possibly related with metabolism optimization and adaptation to stress, as well as proteins involved in plasmid stabilization through postsegregational killing or partitioning systems. For example:

**Cluster 1:**  hypothetical protein, Dienelactone hydrolase-related enzyme and RcgA family putative transporter/Transmembrane protein.  Dienelactone hydrolase-related enzyme catalyzes the breakdown of cyclic ester, and it has been reported with the potential to degraded PET. On the other hand, RcgA was described as a transmembrane protein important for the conjugation of plasmids in *Rhizobium favelukesii* [Castellani et al. (2026)](https://doi.org/10.1128/spectrum.03242-25) 

**Cluster 4**: 'Peptidase C14 caspase catalytic subunit p20', 'Alpha/beta hydrolase', 'DDE superfamily endonuclease;IS630 family transposase;transposase;Tc1-like transposase DDE domain-containing protein' --- 'Peptidase C14 caspase catalytic subunit p20' -> found in Caspases (Cystein ASPartate-specific proteASES), 'Alpha/beta hydrolase' -> diverse bond catalytic.

**Cluster 10:** 'Peptidase;insulinase family protein;pitrilysin family protein;Peptidase M16 domain protein', 'hypothetical protein', 'Transposase;Transposase IS110;IS110 family transposase'

**Cluster 11:** 'MFS transporter', 'aminotransferase class I/II-fold pyridoxal phosphate-dependent enzyme', 'SDR family NAD(P)-dependent oxidoreductase;Alcohol dehydrogenase;SDR family oxidoreductase'

**Cluster 12:** 'hypothetical protein', 'Uncharacterized conserved small protein', 'type II toxin-antitoxin system RelE/ParE family toxin;XRE family transcriptional regulator;Phage-related protein' --- 

**Cluster 13:** 'hypothetical protein;response regulator transcription factor;Helix-turn-helix transcriptional regulator;LuxR family transcriptional regulator', 'Transcriptional regulator MucR family;hypothetical protein;MucR family transcriptional regulator;MucR', 'magnesium/cobalt transporter CorA;Magnesium transporter;magnesium and cobalt transport protein CorA;Magnesium and cobalt transport protein CorA;hypothetical protein' --- 

**Cluster 15** 'PLP-dependent aminotransferase family protein;Aminotransferase class I/II-fold pyridoxal phosphate-dependent enzyme', 'LysR family transcriptional regulator', 'MFS transporter' --- 'Lipocalin-like domain-containing protein', 'cyclophilin-like fold protein', 'hypothetical protein'

**Cluster 16**: 'Heavy metal-binding protein', 'Periplasmic heavy metal sensor', 'Crp/Fnr family transcriptional regulator'  **---**  'efflux RND transporter permease subunit;Copper/silver efflux system membrane component', 'Transmembrane protein', 'Transmembrane protein' **---** 'copper chaperone CopZ', 'Cu(I)-responsive transcriptional regulator', 'hypothetical protein;TetR/AcrR family transcriptional regulator'



> [!question]
> I find the  structural variation approach interesting to find mobile element. I am sure if relationships are correctly established. So far, it seems that transposons could be treated as paralogs as long as they have different neighbors 
> 
> ![[panaroo_gene_fam_collap.png|200]]
> *"Panaroo uses context and a lower clustering threshold to combine diverse gene families into a single gene"*




## *Sinorhizobium meliloti* Can Acquire Defenses Systems Through Accessory Plasmids

The annotation of ArdC during Toxin-Antitoxin system, which has been linked to protection against (RM) systems [Belogurov et al., 2000], led us to investigated whether _S. meliloti_ strains can acquire defense systems, including RM systems. As observed previously, accessory plasmids can carry TA systems, which promote plasmid addiction through post‑segregational killing. Similarly, plasmids can harbor type II RM systems, which can enhance stability via an analogous mechanism: methylation of host DNA prevents endonuclease cleavage [Tsang et al., 2017]. Beyond metabolic genes, plasmids may also carry determinants of antibiotic resistance, phage protection, and interspecies competition.

Interestingly, most defense systems were concentrated on pSymA and the chromosome, with only a few strains harboring defense systems on pSymB. SoFIC, RM Gabija, and SanaTA were the most common defense systems. Similarly, the accessory plasmids most frequently carried Gabija, RM, and CBASS. The presence of RM systems suggests that _S. meliloti_ can acquire them via horizontal gene transfer (HGT), for example through accessory plasmids.

Among RM types, we found type I, II, and IV, with type II being the most common (13/100). Likewise, on the chromosome and megaplasmids, type II RM was also the most frequent (78/256). This contrasts with the prevailing view that _S. meliloti_—and perhaps the entire genus—carries only type I RM. Notably, 15 genomes and two plasmids harbored a type IV RM system, which functions oppositely by cleaving methylated DNA. Type III and type IV were the rarest overall.

Notably, pSymA exhibits a conserved structure comprising SoFIC and the anti-RM protein ArdB. SoFIC was recently shown to provide robust phage protection in bacteria through AMPylation [Wu et al., 2025]. ArdB belongs to a family of anti-restriction proteins known to protect against type I RM systems [Kudryavtseva *et al.* 2023](https://doi.org/10.3389/fmicb.2023.1133144) ; [Serfiotis-Mitsa *et al.* 2010](). In contrast, the accessory plasmids most commonly carried _ardC_ as the anti-RM gene. While ArdB protects against type I RM (which cleaves single-stranded DNA), ArdC has been shown to protect against type II RM (which cleaves both single- and double-stranded DNA) [Belogurov et al., 2000].

This presents an event of possibly plasmid coevolution, the megaplasmid likely became established before type II RM systems spread through populations. Once type II RM became widespread, ArdB could no longer provide protection, possibly explaining why accessory plasmids instead carry _ardC_.


For simplicity, the plot below shows only the MAG genomes.




![[defense_type_MAG_genomes.png | 600]] 
![[defense_type_acc_pls.png | 600 ]]


## Accessory Plasmids Carry Diverse Signal Peptide-Bearing Proteins Involved in Host Fitness

A total of 229 plasmids encoded signal peptide-bearing proteins shorter than 200aa, as identified using SignalP 6.0. These proteins were clustered by the protein families established by PPanGGoLin during pan-genome creation. The heatmap below shows the top 20 protein families more common among the accessory plasmids. We can see transporter substrate-binding related proteins probably enhancing substrate uptake for the host, nuclease-like proteins which have been associated with a diverse of role for survival and adaptation involved from tissue infection to horizontal gene transfer events [Sharma et al. (2019)](https://doi.org/10.1016/j.ijmm.2019.151354).  Interestingly, it has been observed that pathogens can use nuclease to degrade the DNA backbone of extracellular traps that can be produced in the inmune response of humans and even in some plants [Liag et al. (2022)](https://doi.org/10.3389/fimmu.2022.899890) [Tran et al. (2016)](https://doi.org/10.1371/journal.ppat.1005686) [Park et al. (2019)](https://doi.org/10.1128/mbio.02805-18) [Hawes et al. (2011)](https://doi.org/10.1016/j.plantsci.2011.02.007) 

On the other hand, lipoproteins have been associated with pathways that modulate symbiosis. [Bustamante et al. (2023)](https://doi.org/10.1371/journal.pgen.1010776) demonstrated that deletion of _lppA_, a 148-amino-acid lipoprotein, reduced exopolysaccharide‑I (EPS‑I) production and consequently decreased competitive fitness during host colonization. Likewise, succinoglycan biosynthesis protein ExoI - a protein involved in EPS-I production that is required for functional nodule formation- was also among the top 20 proteins identified [Maillet et al. (2019)](https://doi.org/10.1111/tpj.14625) .



> [!question]
> 
> Lipoprotein involved in symbiosis? https://doi.org/10.1371/journal.pgen.1010776

![[protfams_w_signalp_uniq_pls.png]]

## Accessory Plasmids Are Enriched in NonRibosomal Peptide Synthetases 

AntiSmash predicted Biosynthetic Gene Clusters (BGC) on 194 plasmids. BGC are clusters of genes that encode for secondary metabolites which constitutes a rich source for bioactive compounds with potential pharmaceutical value [cite here]()

NonRibosomal Peptide Synthetases (NRPS), NI-siderophore, terpene and hserlactone among the most common. Non-ribosomal peptides (NRPs) has gained attention for their numerous industrial and research applications, such as antimicrobial control against plant pathogens [lacovelli et al. (2021)](https://doi.org/10.1093/jimb/kuab045) [Fira et al. (2018)](https://doi.org/10.1016/j.jbiotec.2018.07.044) [Ranjan et al. (2023)](https://doi.org/10.3390/fermentation9070597). Unlike the chromosome and the megaplasmid, NRPS is the predominant category of BGC in the accessory plasmids. The most common NRPS was related with *Solanimycin non-ribosomal peptide synthetase SolG*, interestingly Solanimycin has been described as powerful antifungal

NI-siderophore are compounds with high affinity for insoluble ferric iron [Schalk et al. (2025)](https://doi.org/10.1038/s41579-024-01090-6) , therefore it allows bacteria and plants to acquire Iron that under alkaline and neutral pH tends to be insoluble [Si et al. (2025)](https://doi.org/10.1093/ismejo/wraf280) 


![[antismash_pred_type_frequency.png]]
![[antismash_pred_type_freq_genome.png|600]]


## Antimicrobial Peptides in Accessory Plasmids (disappointed)

To investigate Antimicrobial peptides (AMP) in our dataset of accessory plasmids we used pyAMPA, Macrel and AMPlify. Macrel and AMPlify had a low output, with only around 5 proteins predicted each. pyAMPA had a highest number of predictions.

![[amp_pyamp_uniq_pls.png]]

Out of pyAMPA predictions only 88 proteins presented a signal peptide (Signalp6)

![[amp_pyamp_w_signalp_uniq_pls.png | 500]]


## Horizontal Gene Transfer Between Accessory Plasmids And Plasmids in the PLSDB

To investigate horizontal gene transfer (HGT), first, all plasmids that had at least a 500 bp match were retrieved from the PLSDB using Minimap2. Subsequently, the weighted Gene Repertoire Relatedness (wGRR) as describe in [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3) was used. Briefly, wGRR take into account the number and identity of the bi-directional best hits (BBH) between all pair of plasmids. It return values between 0 and 1. It will be high when BBH are a large fraction of the smallest element and the proteins are very similar. wGRR is particularly useful to extract proteins related with HGT looking for low global wGRR values and high identity values.  

![[num_pls_per_genus_lt500kb.png]]

![[Len_pls_lt500kb_per_genus.png]]

In order to explore HGT, having computed the wGRR between all-vs-all plasmids, we filtered for plasmids with 0.01 < wGRR < 0.1 as suggested by [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3). The pie below plots the top 10 mean percentage of connections per plasmids in our dataset. We observed that most HGT recovered by this metric are between members of the same order Rhizobiales/Hyphomicrobiales with 7 out of 10 belonging to the Rhizobiaceae family. This reflects that accessory plasmids presents highly host-linage restriction to the family and even to genus level. Interestingly, this is in line with recent experimental and bioinformatics analyses suggesting that plasmid conjugation is biased toward host kin, where plasmid transfer is limited by the host defense systems [Dimitriu et al. (2019)](https://doi.org/10.1098/rspb.2019.1110)  and molecular compatibility, for example, studies in the conjugable plasmids IncF demonstrated that their conjugation is heavily mediated by the interaction between outer membrane proteins encoded by the plasmid's donor and the recipient [He et al. (2026)](https://doi.org/10.1128/jb.00536-25) [Low et. al (2022)](https://doi.org/10.1038/s41564-022-01146-4) 

![[pie_genus_connections_uniq_pls.png|600]]
We can observe the top 20 plasmid clusters ranked by number of plasmids in the group.

![[HGT_net_FR_layout.png|600]]

We can also observe difference in connections by dataset

![[HGT_net_FR_layout_by_dataset.png|600]] 


## LIONESS Single-sample network versions   (JUST AN IDEA)

Create single-version of networks with LIONESS. This might help us visualize how the samples interactions differ when plasmids are removed. In this case, I do not have phenotypic outcomes, so everything would be just function-based. 

LIONESS does not reconstruct networks. It integrates existing reconstructions to estimate. A common scenario are Pearson correlation network using transcriptomic data, which turns out to be relevant for us, as we can create gene correlations.





# What makes *Sinorhizobium meliloti* plasmids large plasmids?


The low acquisition of TA systems, the high prevalence of partition proteins among them, the reduced coverage observed during isolates sequencing, goes directly into a classic question: What is making *S. meliloti*'s plasmids so large? I like the image below retrieved from [Hall *et al.* (2022)](https://doi.org/10.1098/rstb.2020.0472) which presented an interesting overview of the features that makes a plasmid a mega-plasmid.

![[What_makes_megaplasmid.png]]





# Methods

## Genome Assembly and Annotation

A total of 258 strains were analyzed with PacBio HiFi and 95 with Oxford Nanopore (ONT) and assembled. Presenting quality metrics (attach GC, length, contig number, distributions, BUSCO or CheckM completeness). As expected, PacBio’s assemblies achieved higher contiguity than ONT as well as higher accuracy at similar average coverage.

PacBio HiFi reads were filtered using Fastp-long v0.4.1 using default options. PacBio Hifi and ONT datasets were assembled using Flye v2.9.6-b1802 using -_-pacbio-hifi_ and -_-nano-hq_, respectively. ONT data was further polished using _medaka_consensus_ from Medaka v2.1.1 with model _r1041_e82_400bps_sup_v5.2.0_. Quality metrics were computed using QUAST v5.3.0. Whole-genome Average Nucleotide Identity (ANI) was calculated with FastANI v1.34. The final assemblies were annotated with BAKTA v1.11.4 and PlasAnn v.1.1.6 in the case of plasmids.


## Sequence comparison

Whole genome average nucleotide identity (ANI) using Amino acid identity (AAI) was performed with EzAAI. Tree using Mash distances was built with Mashtree v1.4.6.


## Clustering accessory plasmids

For Clustering there are two approaches to explore:
1. Pling: This is a new tool to cluster plasmids considering the containment as well as insertions and deletions using the 
2. Louvain algorithm: This is a simple approach almost to achieve what COPLA was doing. First we perform an all vs all and then we run Louvain to identify communities.



> [!REMEMBER]
> 
> **This was replaced** it is kept to remember: 
> 
> For clustering accessory plasmids I used ***MGE-Cluster***. 
> 
> I am using 1,775 plasmids belonging to species classified in the core genus from the Alfalfa nodule reported in the study previously mentioned.
> 
> In this [notebook](https://webfs/n/projects/jp2992/MOLNG4331/code/plots_for_grant.ipynb) I made some plots to visualize *Sinorhizobium* plasmids inter and intra species



# The plasmids hidden in the short reads assembly
 
 One of the reasons this project needs to invest in long read technology is that pSymA is not the only hotspot for horizontal gene transfer in *Ensifer* species, accessory plasmids are also be part of the mobilome, exchanging genes between each other.

*Soil origin and plant genotype structure distinct microbiome compartments in the model legume Medicago truncatula*

*Population Genomics of the Facultatively Mutualistic Bacteria Sinorhizobium meliloti and S. medicae*



# References


**This is old.** The literature I have been investigating is in [[Literature Summary]]


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

[8] *Medicago root nodule microbiomes: insights into a complex ecosystem with potential candidates for plant growth promotion**