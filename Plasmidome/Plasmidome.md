

# Objective

PsymA for years has been consider a biggest hotspot for intra-strain variability and accessory gene acquisition by horizontal gene transfer, however it has been found that S. meliloti can also carry accessory plasmids, plasmids that have been proven to also carry competence genes affecting symbiosis. 

During this project, we will collect all the accessory plasmids available for *S. meliloti* along with other assembled in-house and with collaborators, and make a description of the diversity of these plasmids in *Sinorhizobium meliloti*.


```table-of-contents
title: **Table of Content**
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
include: 
exclude: 
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
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


![[number_circular_contigs_per_dataset.png]]


### Contamination

| arker lineage            | Count | Note                                            |
| ------------------------ | ----- | ----------------------------------------------- |
| g__Ensifer (UID3566)     | 225   | -                                               |
| g__Pseudomonas (UID4526) | 1     | MAG154_2_filtered                               |
| o__Rhizobiales (UID3654) | 1     | m64404e_240531_162148.hifi_reads.bc2090--bc2090 |

### Length, GC and Depth Per Chromosome



![[len_QC_distri_all_datasets.png]]

Notice that for some genomes inside the Penn and Dakota datasets if I filtered base on 30x coverage based on my "Other" sequences which represent everything that could be an accessory plasmids, I would lose most of the data, however if I consider, for example, only the chromosome, I lose less than 25% of my data.

Some assemblies caught my curiosity. These have contigs with greater lengths than the mean. They were carrying chromosomes > 4Mb and some cases only presenting only 2 contigs > 1Mb (presumably pSymB is missing). 

For example, I investigate the assembly from **contig_2_P9E10_R3L_R4X** and it matches with *S. meliloti*, however it does not present pSymB. A mapping between the its assembly and a S. meliloti reference revealed that pSymB might be contained inside the Chromosome: [map_to_ref.html](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/dakota_collab_P9/flye_asm/P9E10_R3L_R4X/medaka_polish/map_to_ref.paf.html) 

The table Below the strains that were carrying a Chromosome > 4Mb with the number of contigs > 1Mb:

| sample_id                                       | # contigs > 1Mb |
| ----------------------------------------------- | --------------- |
| P9E10_R3L_R4X                                   | 2               |
| P9F10_G8T_R4X                                   | 2               |
| P9F12                                           | 3               |
| P9G1                                            | 3               |
| P9G10                                           | 3               |
| P9G11                                           | 3               |
| P9G12                                           | 3               |
| P9G9                                            | 3               |
| m64404e_240423_150118.hifi_reads.bc2010--bc2010 | 2               |
| m64404e_240423_150118.hifi_reads.bc2013--bc2013 | 3               |
| m64404e_240423_150118.hifi_reads.bc2069--bc2069 | 3               |
| m64404e_240423_150118.hifi_reads.bc2077--bc2077 | 3               |
| m64404e_240423_150118.hifi_reads.bc2084--bc2084 | 3               |
| m64404e_240423_150118.hifi_reads.bc2090--bc2090 | 3               |
| m64404e_240531_162148.hifi_reads.bc2060--bc2060 | 3               |
| m64404e_240531_162148.hifi_reads.bc2074--bc2074 | 3               |
| m64404e_240531_162148.hifi_reads.bc2076--bc2076 | 2               |
| m64404e_240531_162148.hifi_reads.bc2079--bc2079 | 3               |


> [!question]
> For strains with only two contigs: Is this an assembly error or the pSymB was actually "consumed"?
> Coverage metric looks good and it is circularized... 


### Strains Amino acid Identity (AAI)

To confirm their genetic identity, Mash tree was constructed using 3308 RefSeq genomes from the family _Rhizobiaceae_, which placed all our strains within the genus *Sinorhizobium*, thereby confirming their taxonomic position.


![[tree_rhizobiaceae_w_our_strains.png]]

Likewise, whole-genome similarity estimation using Average Nucleotide Identity (ANI) via FastANI revealed the sequence relationships among all genomes. As expected based on the sampling strategy, the Penn State dataset was the least divergent, followed by the Dakota dataset, with the in-house sequenced genomes showing the highest divergence. 

![[ANI_strains.png]]

Further comparative identity analysis using strain Rm1021 as the reference revealed high proteome coverage (>78%) and average nucleotide identity (>98%) across all genomes. _Sinorhizobium meliloti_ is known to possess an open pan-genome, a characteristic that underpins its high genetic variability. This openness results in a vast repertoire of accessory genes, which have been suggested to support the extensive phenotypic diversity observed within the species [ref 1](https://doi.org/10.1186/1471-2164-12-235), [ref2](https://doi.org/10.1371/journal.pcbi.1004478). 

![[AAI_strains_to_ref.png]]
#### TO DO 📋

⚠️ I have to repeat this using Chromosome.


## Accessory Plasmids general description

### *De novo* Accessory Plasmid contigs identification

Considering the high level of genome fragmentation and the low database representation of *S. meliloti* accessory plasmids, in order to use as much data as possible, a de novo approach to identify accessory plasmids was considered. Sequence Bray-Curtis distances using 3-mer composition were computed with pdist from Scipy package, followed by a PCoA dimensional reduction KMeans Clustering algorithm from scikit-learn was used to establish clusters for further analysis. 



![[de_novo_plasmids_contig_identi.png]]

We observed a clear separation among sequences classified as Chromosome, pSymA, pSymB, and Other—the latter encompassing fragmented sequences or accessory plasmids. Clusters 2, 3, and 0 corresponded clearly to Chromosome, pSymA, and pSymB, respectively. However, the remaining clusters did not consistently align with accessory plasmids. To further investigate, we examined the GC content and length distributions of these clusters using sequences greater than 10kb. The analysis suggested that only cluster 1 likely contains biologically relevant information, nonetheless, cluster 4 was retained in the analysis to account for the possible presence of small plasmids.

![[de_novo_len_gc.png]]



### Plasmid de-replication

MobMess was used for containment-based de-replication. Due to the sequence similarity observed between the megaplasmids—particularly pSymA—and accessory plasmids, the megaplasmids were retained in the analysis to prevent false positives that could arise from fragmented sequences and lead to ambiguous plasmid assignments. 

MobMess is a tool for pan-genome study of plasmidome, it tries to identify *plasmids systems* by establishing containment relationships between plasmids. This strategy allows to handle complex scenario where we have to distinguish between fragments and complete plasmids while keeping as much data as possible. 

Using MobMess, we successfully de-replicated our accessory plasmids. The tool correctly identified points of fragmentation that resulted from sequence ambiguity between the accessory plasmids and mega-plasmids. For example, cluster 129 (red) corresponds to fragments between 12kb-15kb that causes assemblies ambiguities between pSymA (big points) and a group of accessory plasmids (small green points)

![[cluster129.png]]
 caption: size points correspond to sequences binary > 1MB (likely pSym). the color of the edge is the ANI (min. possible value is 90%) 

> [!QUESTION]
> What is that 12kb-15kb fragment?
> 

in MobMess, as expected I am interested in backbone, maximal and compound clusters, but in fragments cluster as well, since due to the use of long reads I expect the plasmids being near-complete but due to the coverage they could not be circularize. So now I have to apply a congruent filter to keep a sample of non-redundant/non-ambiguous plasmids. the following image presents what I call a simple in high level but complex on its details.

![[simple_but_complex.png]]

we have two backbones (light green) connected by a compound cluster (dark green), and one of the backbones is uniquely connected to a maximal cluster (purple). The latter are connected to 3 different fragments cluster coming from the same assembly, that likely is the same plasmid, but it is very fragmented due to a low assembly coverage (mean 10x). The compound cluster is a very interesting point of decision. Probably with other parameters using similarity clustering (check fastaANI below) these plasmids would be clustered together into the same cluster and probably same PTUs by COPLA (I could not install it nor even the database), however here we can see that only two plasmids create the connection between two different plasmid identities.

Fragmented clusters are useful as well, for example, the cluster in the image below shows a group of plasmids that due to low coverage were fragmented down to half of the backbone (light green).

![[example_fragment_cluster.png]]

From this, I can can conclude that MobMess output can help me answer two questions: What is the diversity (backbone and compound)? and What is the distribution (backbone, compound and fragmented)? 

### Plasmid Diversity in S. melolti 


### Plasmid Clustering

Plasmid taxonomy classification is a challenge, different plasmid features have been used to classify plasmids into groups: PlasmidFinder, MOB-Suite, COPLA. The latter introduced the term of Plasmid Taxonomic Unit (PTUs), however COPLA is not maintained software and we could not install the COPLA database needed for PTUs classification. Network-based alternatives to study plasmidome has been proposed [ref](https://doi.org/10.1038/s41467-020-16282-w) [ref](https://doi.org/10.1038/s41396-023-01373-5) [ref](https://doi.org/10.1038/s41467-025-57940-1) [ref](https://doi.org/10.1038/s41467-024-45761-7) [ref](https://doi.org/10.1038/s41396-021-00926-w) [ref](https://doi.org/10.1038/s41467-025-65102-6). Considering the lack of agreement for plasmid clustering, we decided use FastANI for ANI estimation, given that FastANI uses a Mash approach but less sensible to divergent and incomplete draft genomes and The Louvain algorithm for community detection implemented in Python using python-Louvain module


> [!NOTE]
> FastANI looks like a good approach, however, Given that clustering these large plasmids is a challenge as they might represent the fusion of smaller plasmids, I want to create a containment network where distances can give me evolutionary relations between plasmids. I found MobMess, it is a super interesting tool proposal that applies this approach and establish plasmids systems discerning between plasmids backbone genes and cargo genes. These two categories combine to form different plasmids structures. 
> 
> The other aspect to consider is the clustering algorithm. Louvain is popular algorithm for community discovery, however, it has been described that it can produce internally disconnected communities, and an alternative was proposed, the Leiden algorithm.
> 
> Next it is a comparison between: in the left, Vclust + Leiden (resolution=1), and in the right, FastANI + Louvain (resolution=1). In this case Louvain and Leiden produce similar result. I used louvain since it is easier to run in python. they are both using tANI to filter >0.9 however I am plotting every edge with AF>0.7. only 10 clusters are colored.
> ![[fastANI_vs_Vclust.png]]
> 
> We can see that FastANI might be overestimating the ANI. whereas Vclust is underestimating it in some cases.
> 

 




The image below is an example of a systematic problem that shares several genomes from Penn State. This is an ambiguity that can easily confused since it can represent different scenarios in the genome assembly. However, we know it is an accessory plasmid, confirmed by plasmid features, kmer composition and re-sequenced of two of the samples (Liana_052_1_filtered & Liana_056_3_filtered). Additionally, it systematically has a coverage inferior to the chromosome and the symbiotic plasmids. This makes me think of a thought I had before with these large plasmids; low-copy number plasmids that restricted even in the same population. This corresponds to isolates, so either cells started losing them or the plasmid are restricted to subpopulations, vertical domination over horizontal has been mentioned in some paper (I lost them, look for them)

With *S. meliloti* something curious happen, their plasmids are very large > 50kb up to 700kb (WHY???), even more interesting during sequencing of isolates for example for the case of the common ~350kb plasmid *contig_4_m64404e_240531_162148.hifi_reads.bc2049--bc2049* all their strains presents reduction in coverage (around halve total), however Liana_052_1_filtered & Liana_056_3_filtered which were part of the re-sequenced strains are very similar and presents coverage as high as chromosome. Also, they presented another plasmid of 75kb.

![[example_ambiguity_w_acc_pls.png]]



I am trying Vclust and MobMess!: Vclust allows me to achieve similar result as the pipeline used in this [soil plasmidome study](https://doi.org/10.1038/s41467-025-65102-6) . whereas MobMess is an interesting proposal that uses containment network to establish what they call "plasmids systems"

Vclust results are very clustering algorithm dependent. I tried all of them, and Leiden and complete linkage are my favorite. Let's compare it with MobMess.


### Plasmids Counts per dataset


The dataset of 258 genomes was filtered for chromosome coverage (30x) or a pSymA circularized. The reason for this filtering is that since I am using a trained model to predict accessory plasmids, a fragment coming from the PsymB or the Chromosome are easier to predict than one coming from the pSymA.

The dataset was split according to the sequencing run for initial plasmids recovery, which corresponds to: two datasets sequenced with PacBio HiFi and one using ONT. 

`seqkit rmdup` was used to remove identical sequences, for a total 378 sequences. Table 1 presents the number of sequences (putative plasmids) retrieved for each dataset. 

| File Name                | Value | # genomes kept |
| ------------------------ | ----- | -------------- |
| plasmids_penn_state_hifi | 213   | 118            |
| plasmids_dakota_nanopore | 125   | 94             |
| plasmids_in_house_asm    | 40    | 44             |
| Total                    | 378   | 256            |


### Size and GC content distribution


![[len_QC_distri_all_datasets_plasmids.png]]

QC values were 57–60%, and plasmid sizes ranged from 35 kb to 700 kb. The 700-kb plasmids exceed the typical threshold for megaplasmids (~300 kb) and are unusually large for accessory elements. Notably, there are two assemblies containing this large plasmid, one of them presented the chromosome, pSymA, pSymB, and the accessory plasmid itself all circularized, however the other one was recognized as a Type I error. This observation is intriguing and may indicate that this replicon represents a mobilizable megaplasmid, or a recently "evolved" element.

>**Assembly graph with 700kb plasmid**
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9G4/assembly_graph.gfa

>**Assembly graph with False positive**
>/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/flye_asm/m64404e_240531_162148.hifi_reads.bc2049--bc2049/assembly_graph.gfa

### MOB and MPF typing




Our analysis revealed that accessory plasmids in our datasets harbored either MOBP or MOBQ. Interestingly, some plasmids contained both MOB proteins, a rare occurrence for accessory elements. While this initially suggested a possible Type I error (i.e., fragmented sequences from the complete pSymA, which encodes both MOBP and MOBQ), assembly graph inspection confirmed one ~400 kb plasmid with both MOBP and MOBQ as a genuine accessory element, with the pSyms and this plasmid all showing correct assembly and good coverage. A similar case  occurred with a sequence predicted with three MOB proteins (*MOBP,MOBQ,MOBQ*). The assembly graph inspection confirmed It belongs to a ~240kb circular plasmid with a coverage of 240x.


>Assembly graph with 400kb plasmid
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9C10/assembly_graph.gfa

> Assembly graph with 240kb plasmid
>/Volumes/projects/jp2992/MOLNG4331/dakota_collab/P9/flye_asm/P9E7_R3L_R4X_Y9Q/assembly_graph.gfa


> [!QUESTION]
> Can this be a transitioning plasmid?? like an intermedia evolutionary state between an accessory plasmid and a mega-plasmid. two plasmids merged??
> 

> [!NOTE]
> By the way, in the same genome I saw a piece of around 1.5kb with high coverage (~50x), I think it might be a virus. An interesting example of a Genome sequenced when a virus activated. 

| Relaxase Type(s)        | Count | Notes                       |
| ----------------------- | ----- | --------------------------- |
| No detected             | 114   |                             |
| MOBQ                    | 124   |                             |
| MOBP                    | 113   |                             |
| MOBQ,MOBQ               | 24    |                             |
| MOBP,MOBQ               | 2     | ~400kb circular & ~700kb FP |
| MOBP,MOBQ,MOBQ          | 1     | ~240kb circular             |
| Total putative plasmids | 378   |                             |
|                         |       |                             |

| mpf_type | count |
|----------|-------|
| MPF_T    | 277   |
| -        | 101   |



> [!WARNING]
> There is a caveat. Remember that I found possibly contamination retrieved by the RFPlasmid. I did not cleaned this for two reasons: 
> 1. I want to see how it behaves
> 2. I want to build a tool to replace RFPlasmid in that step.


If we check at the genus level of Sinorhizobium we see that...


#### TO DO

**Here I can compare with what MOB proteins has been reported in the genus or even the family (Rhizobiaceae)**

### RepABC


> [!WARNING]
> There is a caveat. Remember that I found possibly contamination retrieved by the RFPlasmid. I did not cleaned this for two reasons: 
> 1. I want to see how it behaves
> 2. I want to build a tool to replace RFPlasmid in that step.

Through the annotation of the putative plasmids we could identified the module RepABC for most of the plasmids, just a few could only be annotated for one or two of the Rep proteins.

![[num_repABC_putative_pls.png]]


### Toxin-Antitoxin (TA) systems


> [!WARNING]
> There is a caveat. Remember that I found possibly contamination retrieved by the RFPlasmid. I did not cleaned this for two reasons: 
> 1. I want to see how it behaves
> 2. I want to build a tool to replace RFPlasmid in that step.

To annotate TA systems, the HMM models from TASmania were used. Currently there are two ways to annotate TA systems, using the highly curated TADB or using the more "discovery-oriented. TASmania present higher sensitivity than TADB, however, TASmania  models were built mining for interpro annotated TA in more than 41k assemblies, therefore it has a higher risk of false positive. Using TASmania models, [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) annotated TA systems for approximately 10k plasmids, subsequently trained a Random Forest model which achieved 95% accuracy predicting PTUs. ParB/RepB/Spo0J, Hok/Gef, RelE/ParE, and PemI coding sequences were found among the most influential features for the model accuracy. Interestingly, RepB is the most common plasmid partitioning protein among our plasmids dataset and the annotation more common associated with an antitoxin hit across our plasmids. Functionality variability has been between the proteins in the RepABC, for example, [Ingmer & Cohen (1993)](https://doi.org/10.1128/jb.175.24.7834-7841.1993) demonstrated that RepA can be involved both in plasmid replication and partitioning. Likewise, [Yu *et al.* 2020](https://doi.org/10.1101/2020.11.01.361691) trained PlasX, a logistic regression model, using the gene families to identified plasmid sequences from chromosomal ones. Authors reported PlasX often assigned higher model coefficients to genes strongly associated with plasmid biology, such as the genes for plasmid replication, *repL*, and partitioning, *parA*.

In addition, [Effe *et al.* (2025)](https://doi.org/10.1038/s41467-025-62473-8) investigate the evolutionary advantage provided by the combination of different persistent strategies that can be found in plasmids. The researches found that an active partition system coupled with a TA system provides the greatest fitness advantage, specially for low-copy extrachromosomal elements. This is specially relevant for *Sinorhizobium meloti* given their sizes distributions and high detection of the whole replication module [[#Size and GC content distribution]] involving more than one instance of proteins in the module.

![[TA_type_vs_length.png]]

**(IT WILL BE REPLACE BY PTUs)** Due to the large number of putative plasmids and the observation of highly similar feature profiles, we applied Hierarchical Clustering using the AgglomerativeClustering function from scikit-learn, and employing Ward's linkage method with a distance threshold of 10 allowing us to reduce redundancy by grouping plasmids with nearly identical features and computing the mean at each group. This clustering approach yielded 111 distinct clusters, which were then used for subsequent plotting and analysis.


![[hierarchical_clust_TA_systems.png]]

[TA composition per contig Heatmap]( https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/TA_system/annotation_heatmap_clustered.png) z-scored row-wise

![[heatmap_TA_systems_clustered.png]]

Additionally, here is the [big heatmap version z-scored row-wise](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/TA_system/annotation_heatmap_all_datasets.png) and a [version with raw counts](https://webfs/n/projects/jp2992/Plasmidome_project_MOLNG_4509/TA_system/annotation_heatmap_all_datasets_count.png)

We could noticed the same effect to that reported by [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) analysis, but interestingly our analysis plasmids started with a greater TA frequency and decrease slower starting at 100 kb. [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206) suggested that larger plasmids can increase competence by presenting more beneficial accessory genes compared to small plasmids, therefore larger plasmids tends to reach a saturation point where TA systems offer little advantage and this can be overcome with the inclusion of other beneficial genes through HGT. Such effect has been observed in the context of Restriction-Modification (R-M) systems, [Shaw *et al.* (2023)](https://doi.org/10.1093/nar/gkad452) found that the escape from type II R-M system was associated with plasmid size and host range, implying that while small plasmids might adapt by small mutations, large plasmids opted to add additional beneficial genes providing higher vertical transmission at the cost of horizontal transfer.

![[TA_freq_vs_length.png]]

Each point represent a plasmids, they are colored according to the Hierarchical Clustering (I should change it for my PTUs). The x axis is plasmids length and y axis the **sqrt** of the TA frequency.


#### TO DO

1. Replace the hierachical clustering by the PTUs.
2. I could use https://github.com/liampshaw/rmsFinder to look for type II R-M system and predict target. 




## Origin of Replication in plasmids

During a [[Comparison of Origin of Replication]] between the 44 strains assembled in house, we observed that the predicted Ori by PlasAnn presented unique k-mer composition to distinguished between accessory plasmids, pSymA, pSymB and the chromosome.

Origin of replication were annotated for all putative accessory plasmids sequences. Below, table summarizes the amount of sequences PlasAnn was abled to identify an oriV. 

| Dataset    | # Annotated | Total |
| ---------- | ----------- | ----- |
| Penn State | 145         | 213   |
| Dakota     | 73          | 125   |
| In house   | 35          | 40    |


Following a annotation a PCA from 6-mer composition of the oriV revealed a higher diversity in oriV 6-mer composition among accessory plasmids compared to the pSymA, pSymB and Chromosome which showed a more conserved composition.

pSymA, pSymB and Chromosome were extracted only from the *in house* dataset. pSymA and pSymB were annotated with PlasAnn, and the Chromosome with BAKTA. So far, this sample can be a good representative dataset since it shows the higher diversity according to the the  [[#Strains Amino acid Identity (AAI)]] analysis, other two dataset possibly due to the isolation experiments might present more related strains.



![[PCA_6mer_ori.png]]


> [!WARNING]
> There is a caveat. Remember that I found possibly contamination retrieved by the RFPlasmid. I did not cleaned this for two reasons: 
> 1. I want to see how it behaves
> 2. I want to build a tool to replace RFPlasmid in that step.

However, once again the oriV is highlighted as an interesting feature to analyze for accessory plasmid sample purity. Inspecting the previous graph looking for *contig_7_m64404e_240531_162148.hifi_reads.bc2049--bc2049* a 700kb contamination described during [[#MOB and MPF typing]], we can noticed it was placed with pSymA group, its most probably source of origin. 


![[PCA_6mer_ori_cont_highligth.png]]



## CDS description

I found the Nod locus annotated on the previous contamination, completely confirmed hahaha.

PlasAnn annotation group genes into 10 categories according to  Gene Ontology (GO), Kyoto Encyclopedia of Genes and Genomes (KEGG) and Gene Orthology Cluster (GOC). The following [heatmap](https://webfs/n/projects/jp2992/stowers-notes/Plasmidome/photos/gene_annotation_heatmap_all_datasets.png) presents the enriched categories for each of the putative plasmids sequences. 

![[gene_annotation_heatmap_all_datasets.png]]

### TO DO

I can add PCA analysis to see how gene content separates them


## BioSynthetic Cluster Genes (AntiSmash)



## Gene exchanges between plasmids

For this I could use the wGRR as describe [here](https://doi.org/10.1038/s41467-024-45757-3) 


# What makes *Sinorhizobium meliloti* plasmids large plasmids?


The low acquisition of TA systems, the high prevalence of partition proteins among them, the reduced coverage observed during isolates sequencing, goes directly into a classic question: What is making *S. meliloti*'s plasmids so large? I like the image below retrieved from [Hall *et al.* (2022)](https://doi.org/10.1098/rstb.2020.0472) which presented an interesting overview of the features that makes a plasmid a mega-plasmid.

![[What_makes_megaplasmid.png]]



#### TO DO

With 



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

**This was replaced** it is kept to remember: 

For clustering accessory plasmids I used ***MGE-Cluster***. 

I am using 1,775 plasmids belonging to species classified in the core genus from the Alfalfa nodule reported in the study previously mentioned.

In this [notebook](https://webfs/n/projects/jp2992/MOLNG4331/code/plots_for_grant.ipynb) I made some plots to visualize *Sinorhizobium* plasmids inter and intra species



# The plasmids hidden in the short reads assembly
 
 One of the reasons this project needs to invest in long read technology is that PsymA is not the only hotspot for horizontal gene transfer in *Ensifer* species,   accessory plasmids are also be part of the mobilome, exchanging genes between each other.

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