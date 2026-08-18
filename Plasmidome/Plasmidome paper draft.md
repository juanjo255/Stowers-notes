**

# General Aesthetics for ASM



# Introduction

  

  
  

Sinorhizobium meliloti is a gram-negative alphaproteobacterium from the family Rhizobiaceae that fixes atmospheric nitrogen in root nodule symbioses with legumes of the genera Medicago, Melilotus, and Trigonella [Kearsley, Sather & Finan (2024)](https://www.cell.com/trends/microbiology/abstract/S0966-842X\(24\)00070-2). Therefore, S. meliloti has long served as a model for bacterial symbiosis studies. Most of our current genomic knowledge about this species comes from the reference strain Rm1021 and Rm2011 which in 2001 was described harboring a multipartite genome with a 3.65 Mb chromosome, and two Sym megaplasmids, a 1.35 Mb named pSymA, and 1.68 Mb megaplasmid pSymB ([Galibert et al., 2001](https://doi.org/10.1126/science.1060966)), their names associated by the localization of symbiotic genes in earlier studies ([Schlaman et al., 1998](https://doi.org/10.1007/978-94-011-5060-6_19)). At the present, it is widely known that pSymA is specialized in the establishment of the symbiosis, carrying most of the machinery necessary for this process, which involves nodulation (nod) and nitrogen fixation (nif, fix) genes ([Barnett et al., 2001](https://doi.org/10.1073/pnas.161294798)), whereas pSymB, although it carries some genes involved in symbiosis - such as the exopolysaccharide biosynthesis -, pSymB has specialized in genes required particularly for free-living fitness, encoding essential functions like solute transport systems, transcriptional regulators, cell protection and among other genes involved in catabolic roles. Notably, pSymB has accumulated chromosome-like features such as essential genes for proper cell growth, and a similar dinucleotide composition and codon usage, in consequence it is often referred as a chromid [Finan et al., 2001](https://doi.org/10.1073/pnas.161294698) ; [Wong, Finan & Golding et al., 2002](https://doi.org/10.1007/s10142-002-0068-0); [diCenzo & Finan, 2015](https://doi.org/10.1007/s00438-015-0998-6) ; [Kearsley et al., 2025](https://doi.org/10.1186/s12915-025-02298-5)). In contrast, pSymA retained more plasmid-like characteristics involving a lower GC content and a higher variability in gene content between strains compared to pSymB ([Barnett et al., 2001](https://doi.org/10.1073/pnas.161294798)), as a result it has been suggested that pSymB is evolutionarily older than pSymA ([Wong, Finan & Golding et al., 2002](https://doi.org/10.1007/s10142-002-0068-0); [Kearsley et al., 2025](https://doi.org/10.1186/s12915-025-02298-5)). Additionally, pSymA presents a high density of mobile genetic elements compared with the chromosome and the pSymB. Therefore, pSymA has been considered a hotspot for genomic rearrangements, generation of novel function ([Galardini et al., 2013](https://doi.org/10.1093/gbe/evt027); [diCenzo & Finan, 2015](https://doi.org/10.1007/s00438-015-0998-6)).

Plasmids are extrachromosomal sequences with an active role in bacterial adaptation to dynamic environments. They provide novel genes or extend genetic redundancy, thereby enhancing stress responses, protection, or metabolic capacity. In bacteria, plasmids can be acquired externally through horizontal gene transfer (HGT) via one of three major mechanisms: transformation, transduction, or conjugation.([Jain et al. 2003](https://doi.org/10.1093/molbev/msg154); [Thomas & Nielsen, 2005](https://doi.org/10.1038/nrmicro1234); [Wang, Guo & Jiang et al., 2025](https://doi.org/10.1038/s41467-025-65840-7))

However, it is widely known that S. meliloti’s strains can carry additional extrachromosomal sequences referred to as cryptic, accessory or simply large plasmids, but little is known about their functions …  ([Mercado-Blanco et al. 1993](https://doi.org/10.1007/BF00245309) [Mercado-Blanco & Toro 1996](https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf); [Lagares et al. 2014](https://doi.org/10.1128/microbiolspec.plas-0005-2013); [Pistorio et al. 2003](https://doi.org/10.1016/S0378-1097\(03\)00454-3); [Roumiantseva et al 2002](https://doi.org/10.1128/AEM.68.9.4694-4697.2002);[Stiens](https://doi.org/10.1128/AEM.72.5.3662-3672.2006) et al. 2006; [Kosier](https://doi.org/10.1111/j.1365-294X.1993.tb00097.x) et al. 1996; [Pistorio et al 2008](https://doi.org/10.1111/j.1574-6941.2008.00509.x)) 

  

# Materials and Methods

## Genome Assembly and Quality Assessment

PacBio HiFi reads were quality-filtered using fastp-long v0.4.1 ([Chen et al., 2018](https://doi.org/10.1093/bioinformatics/bty560)) with default parameters. PacBio HiFi and Oxford Nanopore (ONT) reads were assembled with Flye v2.9.6-b1802 ([Kolmogorov et al., 2019](https://doi.org/10.1038/s41587-019-0072-8)) using flags --pacbio-hifi and --nano-hq, respectively. ONT assemblies were polished with medaka_consensus from Medaka v2.1.1 ([Oxford Nanopore Technologies](https://github.com/nanoporetech/medaka)) using model r1041_e82_400bps_sup_v5.2.0. Assembly quality was assessed with QUAST v5.3.0 ([Gurevich et al., 2013](https://doi.org/10.1093/bioinformatics/btt086)) and genome completeness estimated with CheckM ([Parks et al., 2015](https://doi.org/10.1101/gr.186072.114)) using the Ensifer (UID3566) marker set.

  

## Taxonomic Confirmation of genomes

A Mash-distance phylogeny incorporating 3,308 Rhizobiaceae RefSeq genomes was built with Mashtree v1.4.6 ([Katz et al., 2019](https://doi.org/10.21105/joss.01762)). Additionally, Amino acid identity (AAI) was assessed with EzAAI ([Kim, Park & Chun, 2021](https://doi.org/10.1007/s12275-021-1154-0)) using strain Rm1021 as the reference and whole-genome ANI between strains was calculated with FastANI v1.34 ([Jain et al., 2018](https://doi.org/10.1038/s41467-018-07641-9)).

  

## Accessory Plasmid Identification 

Contigs were first classified by alignment to reference replicons using Minimap2 v2.28-r1209 ([Li, 2018](https://doi.org/10.1093/bioinformatics/bty191)), with each contig assigned to the closest matching replicon (Chromosome, pSymA, pSymB, or Other). Trinucleotide frequencies were computed with Kmertools v0.2.1 (comp oligo -k 3) ([Wickramarachchi & Mallawaarachchi](https://github.com/anuradhawick/kmertools)), and pairwise Bray-Curtis distances were calculated from these 3-mer frequencies using pdist from SciPy ([Virtanen et al., 2020](https://doi.org/10.1038/s41592-019-0686-2)). Dimensionality reduction was performed via principal coordinate analysis (PCoA) implemented in Scikit-bio ([scikit-bio development team](https://scikit.bio)), followed by uniform manifold approximation and projection (UMAP) ([McInnes et al., 2018](https://doi.org/10.21105/joss.00861)) for visualization. Unsupervised clustering was carried out on the Bray-Curtis distances using HDBSCAN ([McInnes, Healy & Astels, 2017](https://doi.org/10.21105/joss.00205)) implemented in scikit-learn ([Pedregosa et al., 2011](https://www.jmlr.org/papers/v12/pedregosa11a.html)), and GC content was computed with Seqkit v2.13.0 ([Shen et al., 2024](https://doi.org/10.1002/imt2.191)).

  

## Plasmid De-Replication

Accessory plasmid sequences from all three in-house datasets were combined with publicly available S. meliloti-related plasmids identified in the PLSDB (2024v2) ([Molano et al., 2024](https://doi.org/10.1093/nar/gkae1095)) using mash distances computed with Mash ([Ondov et al., 2016](https://doi.org/10.1186/s13059-016-0997-x)). Using default values, MobMess ([Yu, Fogarty & Eren, 2024](https://doi.org/10.1038/s41564-024-01610-3)) clusters: backbone, compound, and maximal clusters, were kept only if at least one member is circular and all members are < 1 Mb. Fragment clusters were discarded. Pairwise ANI were computed with FastANI for all retrieved sequences relative and alignment fraction (AF) was calculated using the maximum length of each pair.

  

## RepABC, MOB and MPF Annotation

Relaxase (MOB) and mate pair formation (MPF) types were assigned using mob_typer from MOB-Suite v3.1.9 ([Robertson & Nash, 2018](https://doi.org/10.1099/mgen.0.000206)). RepABC were extracted from the BAKTA annotation ([Schwengers et al., 2021](https://doi.org/10.1099/mgen.0.000685)). 

  

## Pan-Genome and Gene Content Analysis

Pan-genomes were built with Panaroo ([Tonkin-Hill et al., 2020](https://doi.org/10.1186/s13059-020-02090-4)) (70% initial clustering threshold, 90% identity/coverage for final grouping). COG categories were assigned with EggNOG-mapper ([Cantalapiedra et al., 2021](https://doi.org/10.1093/molbev/msab293)). Structural variation clusters were identified with HDBSCAN ([McInnes, Healy & Astels, 2017](https://doi.org/10.21105/joss.00205)) on Jaccard distance matrices projected in 2D using MDS (Multidimensional Scaling) reduction from scikit-learn ([Pedregosa et al., 2011](https://www.jmlr.org/papers/v12/pedregosa11a.html)). Finally, one-vs-rest enrichment between clusters was tested using a linear model coupled with Fisher's exact test followed by Benjamini-Hochberg correction.

## Biosynthetic Gene Cluster and Defense Systems Annotation

BGCs were annotated using antiSMASHv8.0 ([Blin et al., 2025](https://doi.org/10.1093/nar/gkaf334)) and Defense systems using DefenseFinderv2.0.1 ([Tesson et al., 2022](https://doi.org/10.1038/s41467-022-30269-9)). 

## Horizontal Gene Transfer

PLSDB sequences (≤500 kb) were aligned to study plasmids using Minimap2 to retrieve sequences sharing ≥ 500 bp. Weighted Gene Repertoire Relatedness (wGRR) was calculated following [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3). Pairs with 0.01 < wGRR < 0.1 were used for HGT network analysis. Briefly, wGRR takes into account the number and identity of the bi-directional best hits (BBH) between all pairs of plasmids. It returns values between 0 and 1. It will be high when BBH are a large fraction of the smallest element and the proteins are very similar. The network was visualized with Gephi ([Bastian, Heymann & Jacomy, 2009](https://doi.org/10.1609/icwsm.v3i1.13937)) using a Fruchterman-Reingold force-directed layout ([Fruchterman & Reingold, 1991](https://doi.org/10.1002/spe.4380211102)). 

  
  

# Results

  
  

## Genome Assembly Quality and Strain Taxonomic Identity

A total of 256 Sinorhizobium meliloti genomes were assembled from three long-read sequencing datasets using two different technologies: 1) in-house PacBio HiFi, 2) a PacBio HiFi from a collaborator at Penn State University, and 3) an Oxford Nanopore Technology (ONT) from collaborator at Dakota State University. Genome completeness was consistently high across datasets, with the majority of assemblies exceeding 98% completeness (compleness_all_datasets.png). PacBio HiFi in house assemblies achieved the highest contiguity followed by the ONT assemblies and last PacBio HiFi from Penn State. These differences among datasets are mostly due to data coverage. Most assemblies' fragmentation was identified between the megaplasmids and the accessory plasmids (number_circular_contigs_per_dataset.png; example_low_cov.png & example_high_cov.png). Coverage was broadly distributed with a median of 45x among all contigs ( len_QC_distri_all_datasets.png).

All study strains were placed within the genus Sinorhizobium and S. meliloti was the closest species to all samples. Pairwise whole-genome ANI between all genomes exceeded 99% ANI (ANI_strains.png), yet revealed that the Penn State dataset exhibited the highest within-group similarity, followed by the Dakota State dataset, whereas in-house sequenced strains displayed the broadest spread. This is consistent with sample origin: Penn State were collected in human manipulated crops, Dakota State were collected from a wild source, whereas the in-house strains represent a subset of the wild strains collected along Spain, France and Corsica during [Riley et al., 2022](https://doi.org/10.1111/mec.16704) .

Additional comparative analysis using reference strain Rm1021 proteome revealed proteome coverage exceeding 78% and average amino acid identity above 98% across all genomes (AAI_strains_to_ref.png), consistent with the known open pan-genome with a high accessory gene content in S. meliloti [(Galardini et al., 2011](https://doi.org/10.1186/1471-2164-12-235); [Galardini et al., 2015](https://doi.org/10.1371/journal.pcbi.1004478)).

  
  

## Accessory Plasmid Identification

Each contig was classified as Chromosome, pSymA, pSymB, or Other, where the Other category represents putative accessory plasmids or fragmented sequences. Because differences in megaplasmid evolutionary dynamics — such as those distinguishing pSymA from pSymB — can be reflected in biological features including GC content and codon usage, contigs were initially characterized using Bray-Curtis distances of trinucleotide composition, reduced via PCoA and visualized with UMAP.

The analysis produced a clear separation of sequences corresponding to the chromosome, pSymA, pSymB, and Other. Within the Other cluster, HDBSCAN identified three distinct subclusters. Inspection of GC content and sequence length distributions revealed that cluster 1 contained biologically relevant accessory plasmid sequences, while clusters 4 and 5 consisted of short fragmented sequences (<15 kb) derived from other replicons. These findings are consistent with the approach of [Wong, Finan, and Golding (2002)](https://doi.org/10.1007/s10142-002-0068-0), who used dinucleotide signatures to justify designating pSymB as a second chromosome, these results suggest that the analyzed genomes harbor recently acquired additional sequences with genomic signatures distinct from those of the chromosome, pSymB, and even pSymA — despite pSymA being the megaplasmid exhibiting more plasmid-like behavior.

 (trinucleo_contig_comp.png & de_novo_len_gc.png) 

  
  

## Containment-Based De-Replication and Characterization of Accessory Plasmids

To consider the fragmentation/incompleteness of the accessory plasmids due to sequence similarity with the megaplasmids (especially pSymA) producing assembly ambiguities, and keep as much data as possible, MobMess was used for containment-based de-replication including with publicly available S. meliloti-related plasmids identified using mash distances in the PLSDB (2024v2). MobMess identifies "plasmid systems" by modeling containment relationships between sequences, enabling the distinction of complete plasmids from fragments while retaining distributional information and additionally providing extra gene-content relationships between plasmids.  

(mobmess_all_plsdb.png; mobmess_clusters_filtfragments.png). 

After de-replication and filtering, the analysis yielded 101 plasmid clusters encompassing 303 total sequences. Very few clusters were shared between datasets, suggesting ecological or isolated location specificity in plasmid distribution. The Penn State dataset, despite contributing the largest number of sequences, yielded the fewest clusters (9), consistent with the high within-collection strain similarity. In contrast, the in-house dataset, with the greatest strain diversity by ANI, produced 28 clusters from 33 sequences. 

(Table) (mobmess_cluster_types_pre_post_filter.png)

Pairwise ANI revealed that plasmids are unique along most of their length. Observed with most AF falling between 0.2-0.4 with high ANI (>80%) likely related to backbone structures. Accordingly, we retained MobMess's 90% containment-based clusters as discrete plasmid identities for downstream comparisons, as this threshold effectively dereplicates the dataset without over-merging what could represent genuinely distinct plasmids.

(plot2_kdeplot_ani_vs_af.png)

Plasmid’s GC content ranged between 48-65% and sizes fall between 34-749kb (len_GC_uniq_pls_kdeplotpng.png), with the largest element (749 kb) representing the largest accessory plasmid reported in this species. 

  
  

## MOB, MPF, and RepABC Annotation: Most Accessory Plasmids Are Conjugable

Most plasmids present a mate pair formation (MPF) system, indicating that most accessory plasmids are self-transferable. Relaxases annotation revealed that MOBQ and MOBP were the two dominant families (mob_typing_uniq_pls_mobmess.png), consistent with previous reports for Rhizobiaceae plasmids [(Redondo-Salvo et al., 2020](https://doi.org/10.1038/s41467-020-17278-2)). 

(Table)

Plasmid sizes in extensively sequenced bacterial species often follow bimodal distributions, with a local minimum between 20-30kb, reflecting the separation between small mobilizable and large conjugative plasmids ([Simillie et al., 2010](https://doi.org/10.1128/mmbr.00020-10)), however, the S. meliloti plasmidome in this collection deviates from this pattern. Instead, 95% of plasmids concentrate above 70 kb, a size distribution consistent with the high prevalence of MPF systems, which, due to size constraints, must rely exclusively on conjugation for horizontal transfer ([Hall et al., 2022](https://doi.org/10.1098/rstb.2020.0472)).

Some unusual cases presented multiple relaxase types. A ~400 kb circular plasmid (P9C10) harbored both MOBP and MOBQ, confirmed by assembly graph inspection as a genuine accessory element with pSymA, pSymB, and chromosome all correctly resolved and well-covered (mean 134x). Similarly, a ~240 kb circular plasmid (P9E7_R3L_R4X_Y9Q) with 240× coverage, contained three relaxase domains (MOBP, MOBQ, MOBQ). Both cases likely represent cointegrate products with MGE harboring different MOB types.

Correspondingly, 289 carried at least one repA gene and 284 contained a complete repABC operon. Thirteen sequences lacked an explicit repABC operon; 11 carried related partition/replication annotations (ParB/RepB/Spo0J family partition protein, ParA protein), possibly suggesting divergent replication modules. RepA was used to assess replicon group diversity.

(pls_features_stackbar.png).

  
  

## Replicon Typing Defines Sinorhizobium-Specific Replicon Groups

  

Replicon type and MOB type based plasmids have been the gold standard for plasmid clustering. plasmids. Particularly the former provides information about plasmid incompatibility. Incompatibility between plasmids comes when they share the same replication and/or partition system which makes them compete in the same cell [(del Solar et al., 1998](https://www.ncbi.nlm.nih.gov/pubmed/9618448)). Although the incompatibility groups has been extensively established for plasmids in the order Enterobacterales [(Orlek et al., 2023](https://doi.org/10.1016/j.plasmid.2023.102684)), in soil α-Proteobacteria such as S. meliloti, plasmid replication and partition are dominated by the repABC family, which is largely absent from Enterobacteriaceae and has not been integrated into the canonical Inc scheme ([Cevallos et al., 2008](https://doi.org/10.1016/j.plasmid.2013.08.001); [Caratolli et al., 2014](https://doi.org/10.1128/aac.02412-14)). However, these classification schemes poorly capture the genomic similarity between plasmids, therefore alternative approaches has been described ([Garcillan-Barcia et al., 2023](https://doi.org/10.1016/j.plasmid.2023.102684))

Therefore, to explore the replicon diversity in these strains of S. meliloti,  repA sequences were extracted and clustered following the same criteria as [Cavassim et al., (2020)](https://doi.org/10.1099/mgen.0.000351) and [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25), during classification of Rhizobium leguminosarum replicon groups. Rh group representatives from the same studies were included during clustering. A total of 36 plasmids clustered with Rh07 and 52 with Rh08, suggesting plasmid exchange between Rhizobium and Sinorhizobium. The remaining 205 sequences formed 15 novel Sinorhizobium-specific clusters designated Si01–Si15 in order of decreasing abundance 

(replicon_groups.png; repl_group_each_strain_heatmap.png). 

  
  

## Gene Content Shared Between Accessory Plasmids And Main Replicons

Gene redundancy has been identified across different bacteria species and linked to an important source for functional innovation, mutation resistance and environment adaptation ([Wang et al., 2025](https://doi.org/10.1038/s41467-025-65840-7);[Fajardo et al., 2023](https://doi.org/10.1038/s41598-023-29800-9); [Qian et al. 2014](https://doi.org/10.1101/gr.172098.114)), S. meliloti high gene content redundancy have been found ([diCenzo & Finan, 2015](https://doi.org/10.1007/s00438-015-0998-6)), thus we investigated the gene content sharing between accessory plasmids and the main replicons. However, if proteins seem to have a similar molecular function according to the amino acid similarity, they can perform unique biological roles that do not complement, such as the case of the five Cu+-ATPases [Patel et al. (2014)](https://doi.org/10.1099/mic.0.079137-0). Accordingly, to do the comparison proteins were clustered at 80% coverage and identity. Also, we only consider genomes presenting circular chromosomes and the megaplasmids, and accessory plasmids were filtered accordingly. At the end we counted 172 genomes and 204 accessory plasmids.

Figure ## shows that pSymB shares more genes with the chromosome, whereas pSymA shares more genes with the accessory plasmids, reflecting their evolutionary differences where, as mentioned before, pSymB reaches a more conservative status of chromid and pSymA keeps more plasmid-like features with gene content flexibility. Interestingly, the chromosome seems to share more genes with the accessory plasmids than the pSymA.

Among the genes most frequently shared across all replicons—excluding transposases and hypothetical proteins—we observed notable functions including the chaperone GroEL/GroES, adenylyltransferase (GlnE), and thioredoxin. These proteins are implicated in proteostasis and protein aggregation control (GroEL/GroES; [Taguchi et al., 2023](https://doi.org/10.3389/fmolb.2023.1091677)), nitrogen metabolism and symbiosis (GlnE; [Rehm et al., 2010](https://doi.org/10.1016/j.jbiotec.2009.11.024), and redox-stress response (thioredoxin; [Alloing et al., 2018](https://doi.org/10.3390/antiox7120182)).

 (gene_sharing_upset.png).

  
  

## MGE Cointegrates Might Be Involved in Large Accessory Plasmids Formation in Sinorhizobium meliloti

Mobile Genetic Elements (MGE) cointegrate is an important evolutionary mechanism in plasmids that confers multiple advantages, by reorganizing plasmids, it diversifies gene content, protects against plasmids incompatibility, enables cross-host transfer of non-conjugative plasmids and can amplify antimicrobial resistance by creating multidrug resistant megaplasmids ([Pesesky et al., 2019](https://doi.org/10.1016/j.plasmid.2019.02.003)  [Wang et al., 2021](https://doi.org/10.3389/fmicb.2021.754931); [Liu et al., 2025](https://doi.org/10.1093/jac/dkaf309); [Ipoutcha et al., 2026](https://doi.org/10.64898/2026.01.09.696371); [de Souza et al., 2026](https://doi.org/10.1007/s00284-026-04819-z)).

During RepABC annotation, there were some instances of multiple RepABC or related annotations. The latter combined with the right-skewed size distribution of S. meliloti accessory plasmids towards large plasmids (>100kb) could be a signal of plasmid fusion events. Additionally, the containment network provided direct evidence for specific fusion events. A ~314 kb plasmid seems to correspond to the fusion of two plasmids (~158 kb and ~146 kb) mediated by a Tn3-family transposase, which is are among the mobile elements most strongly associated with cointegrate formation [(Szuplewska et al., 2014](https://doi.org/10.1080/2159256X.2014.998537)). Similarly, also flanked by a Tn3-family transposase, a ~149 k b plasmid seems to be a cointegrate between a ~73 kb plasmid and other type of MGE, possibly an Integrative Mobilizable Element (IME), based on the presence of integrases/recombinases, a relaxase and conjugation related proteins, and no replication proteins. Consistently, analysis of IS composition per plasmid cluster revealed differences between enrichment of specific IS families in distinct accessory plasmid clusters, which can promote gene exchange between sequences with similar IS families composition, which could end up in MGE cointegration  ([Harmer et al., 2014](https://doi.org/10.1128/mbio.01801-14); [Hua et al., 2020](https://doi.org/10.1080/22221751.2020.1773322)).

(num_repABC_per_pls_plasAnn.png).

(pls_fusion_example.png) (pls_fusion_2.png) (IS_comp_per_cluster.png; IS_comp_per_pls.png).

Interestingly, we identified four strains in which the pSymB megaplasmid and the chromosome appeared to have fused: two from the Dakota State dataset and two from the Penn State dataset. These strains harbored a single large chromosome, a pSymA, and several accessory plasmids, with no independent pSymB replicon detected. Instead synteny analysis revealed pSymB inside of the Chromosome (supplementary: dot plot.png; IGV or pretty Synteny plot). As aforementioned, the megaplasmid pSymB has been suggested as evolutionarily older than pSymA, presenting chromosome-like features, and therefore referred to as a Chromid ([Wong et al., (2002)](https://doi.org/10.1007/s10142-002-0068-0); [diCenzo et al., 2013](https://doi.org/10.1128/jb.01758-12); [diCenzo et al., 2016](https://doi.org/10.1111/1462-2920.13221); [Kearsley et al., 2025](https://doi.org/10.1186/s12915-025-02298-5)). Given its chromosomal similarity, fusion between these two replicons is plausible, and has been documented in other bacteria ([Liao et al., 2022](https://doi.org/10.1016/j.cub.2022.06.050); [Mori et al. 2022](https://doi.org/10.1128/spectrum.02225-21)).

  
  

## Gene Content Profiles Indicates Different Ecological Pressures between Accessory Plasmids

Accessory plasmids are thought to provide fitness improvement in complex ecological environments such as in the soil microbiome [(Hall et al., 2022](https://doi.org/10.1098/rstb.2020.0472)), and particularly for S. meliloti, it has been proposed that accessory plasmids might provide advantages over strains lacking these elements ([Sanjuan & Olivares, 1989](https://doi.org/10.1128/jb.171.8.4154-4161.1989); [Schuleter et al., 2007](https://doi.org/10.1111/j.1574-6968.2007.00731.x)).  

COG (Clusters of Orthologous Groups) annotation revealed accessory plasmids are highly rich in function related with regulation and metabolism related functions such as biosynthesis, transport and catabolism. Notably, there is a high number of genes with unknown function, highlighting the need to increment the efforts to understand their roles in their host fitness.

(COG_plasmids.png)

Although replicon-based and MOB-based clustering are widely used to capture plasmids with similar biological features, these approaches have been shown to correlate poorly with plasmid gene content [(Douarre et al., 2020](https://doi.org/10.3389/fmicb.2020.00483); [Orlek et al., 2017](https://doi.org/10.3389/fmicb.2017.00182); [Redondo-Salvo et al., 2020](https://doi.org/10.1038/s41467-020-17278-2)). Therefore, considering the high proportion of proteins with unknown function, we wonder whether there are differences in gene content between plasmids that might reflect the specific ecological pressures hosts are undergoing. Using Jaccard distance metric on the plasmids pan-genome, we observed a clear difference between plasmids forming discrete clusters, and some clusters which, despite being different according to the MobMess cluster, seems to have a similar gene content, similar to studies in other soil bacteria species ([Gorbitz et al. 2025](https://journals.asm.org/doi/10.1128/mbio.02497-25#sec-4)).

To determine whether the accessory plasmid exhibit specific protein organization that characterize their ecological niche, we leveraged the structural variation information provided by Panarroo during pan-genome construction. Several of the structural variations identified were associated with genes related with transcriptional regulators, and membrane proteins, potentially related with metabolism optimization and adaptation to stress, as well as proteins involved in plasmid stabilization through postsegregational killing or partitioning systems (supplementary:excel with retrieved plasmid’s conserved protein paths).

For example, Cluster 11 encodes a structural variation linking an MFS transporter, a PLP-dependent aminotransferase (class I/II fold), and an SDR family NAD(P)-dependent oxidoreductase (alcohol dehydrogenase-like). This combination suggests a metabolic cassette involved in amino acid catabolism and redox balance, with the MFS transporter potentially mediating efflux of metabolic intermediates or toxic compounds—functions broadly relevant to nutrient acquisition and stress adaptation. Cluster 16 presents a conserved structure related with heavy metal-binding proteins ('Heavy metal-binding protein', 'Periplasmic heavy metal sensor', 'Crp/Fnr family transcriptional regulator') suggesting heavy metal tolerance which is ecologically relevant in soil-dwelling rhizobia, where metals like copper are common for instance in agricultural soils.  (supplementary:excel with retrieved plasmid’s conserved protein paths)

(gene_content_pls_MDS_panaroo.png) (SV_MDS_uniq_pls.png)

  
  

## Accessory Plasmids Carry Diverse but Not Abundant Toxin-Antitoxin Systems

In addition to requiring a functional replication module to persist within the cell, plasmids can encode extra mechanisms for stability, including multimer resolution, active partition systems, and plasmid addiction or toxin-antitoxin (TA) systems that ensure vertical transmission by establishing a host dependence. This is especially needed by large plasmids which are often found in low copy numbers, and it has been proposed that the combination of an active partition system coupled with a TA system provides the greatest fitness advantage ([Luchetti et al. 2023](https://doi.org/10.1371/journal.pone.0318411);  [Effe et al. 2025](https://doi.org/10.1038/s41467-025-62473-8)).

TA system accumulation decreased with increasing plasmid size ( TA_type_vs_length.png; heatmap_TA_systems_clustered.png; heatmap_TA_systems_mean_clustered.png), replicating the pattern reported by [Bethke et al. (2023)](https://doi.org/10.1093/molbev/msae206). This is consistent with the interpretation that larger plasmids complement TA systems acquiring other beneficial accessory genes, a pattern also documented for restriction-modification (R-M) systems [(Shaw et al. 2023](https://doi.org/10.1093/nar/gkad452)). 

Notably, the most common annotation among TA models was RepB or partition-related protein. This may reflect the fact that TA systems can be part of the plasmid backbone and be located in proximity to the replication module ([Yamamoto et al., 2009](https://doi.org/10.1128/jb.00124-09); [Luchetti et al., 2023](https://doi.org/10.1371/journal.pone.0318411); [Yu, Fogarty & Eren, 2024](https://doi.org/10.1038/s41564-024-01610-3)), particularly given that TASmania models are a set of models "discovery-oriented" that offer higher sensitivity than TADB at the cost of a possible high false positive rate [(Akarsu et al., 2019](https://doi.org/10.1371/journal.pcbi.1006946)), 

  

Alternatively, functional variability has been reported in the proteins of the RepABC, just like [Ingmer & Cohen (1993)](https://doi.org/10.1128/jb.175.24.7834-7841.1993) demonstrated that RepA can be involved both in plasmid replication and partitioning, however it could also indicate putative anti-toxin, which commonly harbor helix-turn-helix domains, or ancestral gene acquisition, for instance, through plasmids fusion or cointegrate events ([Qu et al., 2019](https://doi.org/10.2147/IDR.S189168); [Wang et al., 2021](https://doi.org/10.3389/fmicb.2021.754931); [Hall et al., 2022](https://doi.org/10.1098/rstb.2020.0472)). 

  

The second most frequent annotation was ArdC, which caught our attention as it is not a TA system but an anti-restriction protein of type C. Plasmids frequently carry anti-restriction genes that confer protection against host R-M systems during conjugation ([Dimitriu et al., 2024](https://doi.org/10.1093/nar/gkae896)). In vitro experiments with E. coli demonstrated that ArdC can protect single-stranded DNA against the type II restriction endonuclease HhaI. Consequently, ArdC has been proposed to protect plasmids from host restriction-modification (R-M) systems during conjugation ([Belogurov et al. (2000)](https://doi.org/10.1006/jmbi.1999.3493); [González-Montes et al. (2020)](https://doi.org/10.1371/journal.pgen.1008750)). This finding is noteworthy in the context of Sinorhizobium, as these species were long considered to lack an R-M system. Indeed, the model strain S. meliloti Rm1021 presents only type I R-M flanked by insertion sequences (IS), suggestive of horizontal acquisition ([Capela et al., 2001](https://doi.org/10.1073/pnas.161294398); [Ferri et al., 2010](https://doi.org/10.1016/j.plasmid.2010.01.001); [Dohlemann et al., 2016](https://doi.org/10.1016/j.jbiotec.2016.06.033)).

Finally, we observed common instances of the Type II TA VapC system and the family transcriptional regulator CopG. These represent interesting cases where TA systems may play dual functions beyond their canonical role. CopG has been historically recognized as an actor in the copy number control of conjugative plasmids ([Gomis-Rüth et al., 1998](https://doi.org/10.1093/emboj/17.24.7404) [;Ni et al., 2021](https://doi.org/10.1073/pnas.2011577118)), and was recently identified as an important gene in the symbiosis of Bradyrhizobium sp. SUTN9-2 with legumes [(Wangthaisong et al., 2024](https://doi.org/10.3390/biology13060415)), similarly, VapC has been associated with cold adaptation in Bosea sp. PAMC 26642 ([Jeon, Choi and Hwang, 2021](https://doi.org/10.1261/rna.078786.121)). 

  
  

## Contrasting Anti-R-M Profiles in Core and Accessory Replicons of Sinorhizobium meliloti: Evidence for Horizontal R-M Acquisition and Plasmid Coevolution

  

Beyond metabolic genes, plasmids can carry genes that provide antibiotic resistance, phage protection, and interspecies competition. The prevalence of ArdC led us to investigate whether S. meliloti can acquire defense systems through these accessory plasmids, including R-M systems. As discussed previously, accessory plasmids can ensure plasmid stability by carrying TA systems. Similarly, plasmids can harbor R-M systems, which, in addition to providing cell defense, can enhance plasmid stability in a similar way: methylation addiction, where the methylation DNA prevents endonuclease cleavage ([Kusano et al, 1995](https://doi.org/10.1073/pnas.92.24.11095); [Vasu & Nagaraja, 2013](https://doi.org/10.1128/mmbr.00044-12)). Additionally, Sinorizobium meliloti as part of the accessory genes can carry orphans methyltransferases, which could provide protection against host R-M systems ([Passeri et al., 2025](https://doi.org/10.1093/gbe/evae245)).

Most defense systems were concentrated on pSymA and the chromosome, with only a few strains harboring defense systems on pSymB. SoFIC (221), SanaTA (98), and R-M (97)  were the three most common defense systems on the genomes, whereas on the accessory plasmids, DS-20 (72), Gabija (39), Hachiman (36) were the most prevalent. (defense_type_MAG_genomes.png; defense_type_acc_pls.png)

Although 169 out of 303 accessory plasmids were annotated for an anti-R-M protein ArdC, only 18 presented a R-M type of the types I, II, and IV, with type II being the most common (13). Similarly, among the 97 genomes that presented an R-M system, type II was the most prevalent (78). This contrasts with the prevailing view that S. meliloti carries only type I R-M [(Ferri et al., 2010](https://doi.org/10.1016/j.plasmid.2010.01.001); [diCenzo et al., 2022](https://doi.org/10.1128/mSystems.01092-21); [Passeri et al., 2025](https://doi.org/10.1093/gbe/evae245)). Finally, Fifteen genomes and two plasmids harbored a type IV R-M, considered the rarest R-M system among bacteria. In contrast to types I–III, type IV R-M systems cleave methylated DNA rather than unmethylated DNA. ([Vasu & Nagaraja, 2013](https://doi.org/10.1128/mmbr.00044-12))

Similarly, pSymA (218) carries an anti-R-M protein ArdB, which also provides protection against R-M, particularly type I R-M [(Kudryavtseva et al., 2023](https://doi.org/10.3389/fmicb.2023.1133144)). Considering the narrow host range of these large plasmids, the anti-R-M divergence between pSymA and the accessory plasmids may constitute an event plasmid coevolution ([Harrison & Brockhurst, 2013](https://doi.org/10.1016/j.tim.2012.04.003)): if pSymA was established before type II R-M systems spread through S. meliloti populations, ArdB would have been sufficient, and the later spread of type II R-M may have promoted the acquisition of ArdC by accessory plasmids. Alternatively, prior acquisition of ArdC could have facilitated the host-range expansion from S. meliloti to other Rhizobiaceae, subsequently introducing type II R-M systems into the population. 

Considering the host-restricted nature of Rhizobiaceae plasmids, this observation amplifies the role of methylation systems in S. meliloti, supporting related investigations in other studies ([diCenzo et al., 2022](https://doi.org/10.1128/mSystems.01092-21); [Passeri et al., 2025](https://doi.org/10.1093/gbe/evae245)). This data provides insightful information that could be relevant in S. meliloti transformation through electroporation which can be inefficient due to horizontal barriers, such as those imposed by R-M, as demonstrated during plasmid electroporation experiments in S. meliloti Rm1021 where transformation efficiency increased with non-self DNA in hsdR mutants—a restriction enzyme belonging to a type I R-M system ([Ferri et al., 2010](https://doi.org/10.1016/j.plasmid.2010.01.001); [Dohlemann et al., 2016](https://doi.org/10.1016/j.jbiotec.2016.06.033)).  

The presence of R-M systems on accessory plasmids indicates that S. meliloti can acquire novel defense capabilities via HGT, adding complexity to the conjugation dynamics regulated by methylation patterns and regulatory elements [(Dohlemann et al., 2016](https://doi.org/10.1016/j.jbiotec.2016.06.033); [Passeri et al., 2025](https://doi.org/10.1093/gbe/evae245); [Castellani et al., 2026](https://doi.org/10.1128/spectrum.03242-25); [Brom et al., 2014](https://doi.org/10.1007/978-1-4614-9203-0_3)). 

## Accessory Plasmids Are Enriched in NonRibosomal Peptide Synthetases

Biosynthetic Gene Clusters (BGC) are clusters of genes that encode for secondary metabolites which constitute a rich source for bioactive compounds with potential pharmaceutical value. BGCs were found in 194 accessory plasmids. In contrast to the chromosome and the megaplasmids, Non-Ribosomal Peptide Synthetases (NRPS) is the predominant BGC category in the accessory plasmids, followed by NI-siderophore, terpene and Hserlactone. Non-ribosomal peptides (NRPs) has gained attention for their numerous industrial and research applications, such as antimicrobial control against plant pathogens [lacovelli et al. (2021)](https://doi.org/10.1093/jimb/kuab045) [Fira et al. (2018)](https://doi.org/10.1016/j.jbiotec.2018.07.044) [Ranjan et al. (2023)](https://doi.org/10.3390/fermentation9070597); a notable example is the Solanimycin non-ribosomal peptide synthetase SolG, an observed BAKTA annotation associated with NRPS. Solanimycin is a compound recently described as a strong antifungal compound ([Murphy et al., 2023](https://doi.org/10.1021/acschembio.2c00947)), suggesting accessory plasmids may equip S. meliloti strains with antifungal capabilities relevant for rhizosphere competition. NI-siderophores mediate scavenging of insoluble ferric iron, an important trait under alkaline and neutral soil pH conditions where iron bioavailability is limited ([Schalk et al. 2025](https://doi.org/10.1038/s41579-024-01090-6); [Si et al. 2025](https://doi.org/10.1093/ismejo/wraf280)).

(antismash_pred_type_frequency.png; antismash_pred_type_freq_genome.png)

  
  

## Accessory Plasmids Carry Signal Peptide-Bearing Proteins With Roles in Host Interaction

A total of 229 accessory plasmids encoded proteins shorter than 200 amino acids with signal peptides. The 20 most abundant pan-genome families included substrate-binding related proteins probably relataled to substrate uptake for the host, nuclease-like proteins which have been associated with a wide functional diversity associated with survival and adaptation involving from tissue infection to horizontal gene transfer events, including the degradation of extracellular DNA barriers found during host colonization. In the rhizosphere, such nucleases could similarly facilitate niche establishment by mitigating plant-derived extracellular traps. [Sharma et al. (2019)](https://doi.org/10.1016/j.ijmm.2019.151354); [Liag et al. (2022)](https://doi.org/10.3389/fimmu.2022.899890); [Tran et al. (2016)](https://doi.org/10.1371/journal.ppat.1005686); [Park et al. (2019)](https://doi.org/10.1128/mbio.02805-18); [Hawes et al., 2011](https://doi.org/10.1016/j.plantsci.2011.02.007)). 

Finally, lipoproteins and succinoglycan biosynthesis protein ExoI represented notable annotation among the small secreted proteins. Lipoproteins have been linked with pathways that modulate symbiosis; [Bustamante et al. (2023)](https://doi.org/10.1371/journal.pgen.1010776) demonstrated that deletion of lppA, a 148-amino-acid lipoprotein, reduced exopolysaccharide‑I (EPS‑I) production and consequently decreased competitive fitness during host colonization. Similarly, production of Succinoglycan was found to be involved in EPS-I production and required for functional nodule formation ([Maillet et al., 2019](https://doi.org/10.1111/tpj.14625)). The co-occurrence of both annotations on accessory plasmids suggest a plasmid-encoded contribution to EPS-I regulation and supports their role in symbiotic effectiveness. 

(protfams_w_signalp_uniq_pls.png).

## Horizontal Gene Transfer of Accessory Plasmids Reveal Narrow Host Range

All PLSDB sequences (≤500 kb) sharing at least 500 bp with our plasmid set were retrieved using Minimap2, and weighted Gene Repertoire Relatedness (wGRR) was calculated for all pairs following [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3). wGRR is particularly useful to extract proteins related to the horizontal gene transfer (HGT) looking for low global wGRR values (wGRR < 0.1) and high gene identity values (>0.8).

(num_pls_per_genus_lt500kb.png; Len_pls_lt500kb_per_genus.png)

The vast majority of HGT connections were to plasmids from other Rhizobiales/Hyphomicrobiales, with 7 of the top 10 most-connected genera belonging to Rhizobiaceae which reflects accessory plasmids host-linage restriction to the family and even to genus level. This is in line with recent experimental and bioinformatics analyses suggesting that plasmid conjugation is biased toward host kin, where plasmid transfer is limited by the host defense systems [](https://doi.org/10.1098/rspb.2019.1110)and molecular compatibility [(Dimitriu et al., 2019](https://doi.org/10.1098/rspb.2019.1110)). For instance, studies in the conjugable plasmids IncF demonstrated that their conjugation is strongly mediated by the interaction between outer membrane proteins encoded by the plasmid's donor and the recipient [(He et al., 2026](https://doi.org/10.1128/jb.00536-25); [Low et al., 2022](https://doi.org/10.1038/s41564-022-01146-4)).  

Additionally,  The HGT network reveals the complex web of genetic exchange connecting S. meliloti strains with a broad diversity of bacterial taxa. The network structure demonstrates that accessory plasmids present connections to specific bacterial genera; while effectively expanding the known horizontal gene transfer landscape of this species beyond its genomic relationships, it also exposes distinct patterns of plasmid connectivity with specific taxonomic groups, suggesting that these accessory genetic elements carry lineage-specific signatures of gene exchange, and likely reflecting the ecological histories of individual strains, shaped by the microbial communities of their native environments which may underlie adaptations to specific abiotic and biotic conditions.

This analysis provides critical insight into the role of accessory plasmids in the complex mobilome of S. meliloti. These elements are gene-rich and self-transferable, yet they possess a narrow host range and can harbor MGE defense systems that regulate horizontal transfer. This adds a layer of regulatory complexity that likely promotes the formation of distinct subpopulations that coexist within the same ecological niche.

  

(HGT_net_FR_layout.png; HGT_net_FR_layout_by_dataset.png; pie_genus_connections_uniq_pls.png)

  
  
  
  

  
  

# Discussion 

HELLO

  

# Conclusion

HELLO

  
  
  
  
  
  
  
**


# References

Akarsu H, Bordes P, Mansour M, Bigot D-J, Genevaux P, Falquet L. 2019. TASmania: a bacterial toxin-antitoxin systems database. PLoS Comput Biol 15:e1006946. https://doi.org/10.1371/journal.pcbi.1006946

Alloing G, Mandon K, Boncompagni E, Montrichard F, Frendo P. 2018. Involvement of glutaredoxin and thioredoxin systems in the nitrogen-fixing symbiosis between legumes and rhizobia. Antioxidants 7:182. https://doi.org/10.3390/antiox7120182

Barnett MJ, Fisher RF, Jones T, Komp C, Abola AP, Barloy-Hubler F, Bowser L, Capela D, Galibert F, Gouzy J, Gurjal M, Hong A, Huizar L, Hyman RW, Kahn D, Kahn ML, Kalman S, Keating DH, Palm C, Peck MC, Surzycki R, Wells DH, Yeh K-C, Davis RW, Federspiel NA, Long SR. 2001. Nucleotide sequence and predicted functions of the entire Sinorhizobium meliloti pSymA megaplasmid. Proc Natl Acad Sci U S A 98:9883–9888. https://doi.org/10.1073/pnas.161294798

Bastian M, Heymann S, Jacomy M. 2009. Gephi: an open source software for exploring and manipulating networks. Proc Int AAAI Conf Web Soc Media 3:361–362. https://doi.org/10.1609/icwsm.v3i1.13937

Belogurov AA, Delver EP, Agafonova OV, Belogurova NG, Lee L-Y, Kado CI. 2000. Antirestriction protein Ard (type C) encoded by IncW plasmid pSa has a high similarity to the “protein transport” domain of TraC1 primase of promiscuous plasmid RP4. J Mol Biol 296:969–977. https://doi.org/10.1006/jmbi.1999.3493

Bethke JH, Kimbrel J, Jiao Y, Ricci D. 2024. Toxin-antitoxin systems reflect community interactions through horizontal gene transfer. Mol Biol Evol 41:msae206. https://doi.org/10.1093/molbev/msae206

Blin K, Shaw S, Vader L, Szenei J, Reitz ZL, Augustijn HE, Cediel-Becerra JDD, de Crécy-Lagard V, Koetsier RA, Williams SE, Cruz-Morales P, Wongwas S, Segurado Luchsinger AE, Biermann F, Korenskaia A, Zdouc MM, Meijer D, Terlouw BR, van der Hooft JJJ, Ziemert N, Helfrich EJN, Masschelein J, Corre C, Chevrette MG, van Wezel GP, Medema MH, Weber T. 2025. antiSMASH 8.0: extended gene cluster detection capabilities and analyses of chemistry, enzymology, and regulation. Nucleic Acids Res 53:W32–W38. https://doi.org/10.1093/nar/gkaf334

Brom S, Pistorio M, Romero D, Torres-Tejerizo G. 2014. Boundaries for conjugative transfer of rhizobial plasmids: restraining and releasing factors, p 43–57. In Plasticity in plant-growth-promoting and phytopathogenic bacteria. Springer, New York, NY. https://doi.org/10.1007/978-1-4614-9203-0_3

Bustamante JA, Ceron JS, Gao IT, Ramirez HA, Aviles MV, Bet Adam D, Brice JR, Cuellar RA, Dockery E, Jabagat MK, Karp DG, Lau JK-O, Li S, Lopez-Magaña R, Moore RR, Morin BKR, Nzongo J, Rezaeihaghighi Y, Sapienza-Martinez J, Tran TTK, Huang Z, Duthoy AJ, Barnett MJ, Long SR, Chen JC. 2023. A protease and a lipoprotein jointly modulate the conserved ExoR-ExoS-ChvI signaling pathway critical in Sinorhizobium meliloti for symbiosis with legume hosts. PLoS Genet 19:e1010776. https://doi.org/10.1371/journal.pgen.1010776

Cantalapiedra CP, Hernández-Plaza A, Letunic I, Bork P, Huerta-Cepas J. 2021. eggNOG-mapper v2: functional annotation, orthology assignments, and domain prediction at the metagenomic scale. Mol Biol Evol 38:5825–5829. https://doi.org/10.1093/molbev/msab293

Capela D, Barloy-Hubler F, Gouzy J, Bothe G, Ampe F, Batut J, Boistard P, Becker A, Boutry M, Cadieu E, Dréano S, Gloux S, Godrie T, Goffeau A, Kahn D, Kiss E, Lelaure V, Masuy D, Pohl T, Portetelle D, Pühler A, Purnelle B, Ramsperger U, Renard C, Thébault P, Vandenbol M, Weidner S, Galibert F. 2001. Analysis of the chromosome sequence of the legume symbiont Sinorhizobium meliloti strain 1021. Proc Natl Acad Sci U S A 98:9877–9882. https://doi.org/10.1073/pnas.161294398

Carattoli A, Zankari E, García-Fernández A, Voldby Larsen M, Lund O, Villa L, Møller Aarestrup F, Hasman H. 2014. In silico detection and typing of plasmids using PlasmidFinder and plasmid multilocus sequence typing. Antimicrob Agents Chemother 58:3895–3903. https://doi.org/10.1128/aac.02412-14

Castellani LG, Cabrera MD, Luchetti A, Nilsson JF, Pérez-Giménez J, Bañuelos-Vazquez LA, Alva A, Wibberg D, Busche T, Kalinowski J, Schlüter A, Pühler A, Niehaus K, Pistorio M, Torres Tejerizo G. 2026. Characterization of RcgA and RcgR, two rhizobial proteins involved in the modulation of plasmid transfer. Microbiol Spectr 14:e03242-25. https://doi.org/10.1128/spectrum.03242-25

Cavassim MIA, Moeskjær S, Moslemi C, Fields B, Bachmann A, Vilhjálmsson BJ, Schierup MH, Young JPW, Andersen SU. 2020. Symbiosis genes show a unique pattern of introgression and selection within a Rhizobium leguminosarum species complex. Microb Genom 6:mgen000351. https://doi.org/10.1099/mgen.0.000351

Chen S, Zhou Y, Chen Y, Gu J. 2018. fastp: an ultra-fast all-in-one FASTQ preprocessor. Bioinformatics 34:i884–i890. https://doi.org/10.1093/bioinformatics/bty560

del Solar G, Giraldo R, Ruiz-Echevarría MJ, Espinosa M, Díaz-Orejas R. 1998. Replication and control of circular bacterial plasmids. Microbiol Mol Biol Rev 62:434–464. https://doi.org/10.1128/mmbr.62.2.434-464.1998

de Souza HCA, de Oliveira Almeida AC, Conte-Junior CA, et al. 2026. Multi-replicon architecture drives the global accumulation of resistance to antimicrobials, biocides, and metals in IncF and IncH plasmids. Curr Microbiol 83:241. https://doi.org/10.1007/s00284-026-04819-z

diCenzo G, Milunovic B, Cheng J, Finan TM. 2013. The tRNA(arg) gene and engA are essential genes on the 1.7-Mb pSymB megaplasmid of Sinorhizobium meliloti and were translocated together from the chromosome in an ancestral strain. J Bacteriol 195:202–212. https://doi.org/10.1128/jb.01758-12

diCenzo GC, Finan TM. 2015. Genetic redundancy is prevalent within the 6.7 Mb Sinorhizobium meliloti genome. Mol Genet Genomics 290:1345–1356. https://doi.org/10.1007/s00438-015-0998-6

diCenzo GC, Zamani M, Milunovic B, Finan TM. 2016. Genomic resources for identification of the minimal N2-fixing symbiotic genome. Environ Microbiol 18:2534–2547. https://doi.org/10.1111/1462-2920.13221

diCenzo GC, Cangioli L, Nicoud Q, Cheng JHT, Blow MJ, Shapiro N, Woyke T, Biondi EG, Alunni B, Mengoni A, Mergaert P. 2022. DNA methylation in Ensifer species during free-living growth and during nitrogen-fixing symbiosis with Medicago spp. mSystems 7:e01092-21. https://doi.org/10.1128/mSystems.01092-21

Dimitriu T, Marchant L, Buckling A, Raymond B. 2019. Bacteria from natural populations transfer plasmids mostly towards their kin. Proc R Soc B 286:20191110. https://doi.org/10.1098/rspb.2019.1110

Dimitriu T, Szczelkun MD, Westra ER. 2024. Various plasmid strategies limit the effect of bacterial restriction–modification systems against conjugation. Nucleic Acids Res 52:12976–12986. https://doi.org/10.1093/nar/gkae896

Döhlemann J, Brennecke M, Becker A. 2016. Cloning-free genome engineering in Sinorhizobium meliloti advances applications of Cre/loxP site-specific recombination. J Biotechnol 233:160–170. https://doi.org/10.1016/j.jbiotec.2016.06.033

Douarre P-E, Mallet L, Radomski N, Felten A, Mistou M-Y. 2020. Analysis of COMPASS, a new comprehensive plasmid database revealed prevalence of multireplicon and extensive diversity of IncF plasmids. Front Microbiol 11:483. https://doi.org/10.3389/fmicb.2020.00483

Effe J, Santer M, Wang Y, Feenstra TE, Hülter NF, Dagan T. 2025. The combination of active partitioning and toxin-antitoxin systems is most advantageous for low-copy plasmid fitness. Nat Commun 16:7707. https://doi.org/10.1038/s41467-025-62473-8

Fajardo D, Saint Jean R, Lyons PJ. 2023. Acquisition of new function through gene duplication in the metallocarboxypeptidase family. Sci Rep 13:2512. https://doi.org/10.1038/s41598-023-29800-9

Ferri L, Gori A, Biondi EG, Mengoni A, Bazzicalupo M. 2010. Plasmid electroporation of Sinorhizobium strains: the role of the restriction gene hsdR in type strain Rm1021. Plasmid 63:128–135. https://doi.org/10.1016/j.plasmid.2010.01.001

Finan TM, Weidner S, Wong K, Buhrmester J, Chain P, Vorhölter FJ, Hernandez-Lucas I, Becker A, Cowie A, Gouzy J, Golding B, Pühler A. 2001. The complete sequence of the 1,683-kb pSymB megaplasmid from the N2-fixing endosymbiont Sinorhizobium meliloti. Proc Natl Acad Sci U S A 98:9889–9894. https://doi.org/10.1073/pnas.161294698

Fira D, Dimkić I, Berić T, Lozo J, Stanković S. 2018. Biological control of plant pathogens by Bacillus species. J Biotechnol 285:44–55. https://doi.org/10.1016/j.jbiotec.2018.07.044

Fruchterman TMJ, Reingold EM. 1991. Graph drawing by force-directed placement. Softw Pract Exp 21:1129–1164. https://doi.org/10.1002/spe.4380211102

Galardini M, Mengoni A, Brilli M, Pini F, Fioravanti A, Lucas S, Lapidus A, Cheng J-F, Goodwin L, Pitluck S, Land M, Hauser L, Woyke T, Mikhailova N, Ivanova N, Daligault H, Bruce D, Detter C, Tapia R, Han C, Teshima H, Mocali S, Bazzicalupo M, Biondi EG. 2011. Exploring the symbiotic pangenome of the nitrogen-fixing bacterium Sinorhizobium meliloti. BMC Genomics 12:235. https://doi.org/10.1186/1471-2164-12-235

Galardini M, Pini F, Bazzicalupo M, Biondi EG, Mengoni A. 2013. Replicon-dependent bacterial genome evolution: the case of Sinorhizobium meliloti. Genome Biol Evol 5:542–558. https://doi.org/10.1093/gbe/evt027

Galardini M, Brilli M, Spini G, Rossi M, Roncaglia B, Bani A, Chiancianesi M, Moretto M, Engelen K, Bacci G, Pini F, Biondi EG, Bazzicalupo M, Mengoni A. 2015. Evolution of intra-specific regulatory networks in a multipartite bacterial genome. PLoS Comput Biol 11:e1004478. https://doi.org/10.1371/journal.pcbi.1004478

Galibert F, Finan TM, Long SR, Pühler A, Abola P, Ampe F, Barloy-Hubler F, Barnett MJ, Becker A, Boistard P, Bothe G, Boutry M, Bowser L, Buhrmester J, Cadieu E, Capela D, Chain P, Cowie A, Davis RW, Dréano S, Federspiel NA, Fisher RF, Gloux S, Godrie T, Goffeau A, Golding B, Gouzy J, Gurjal M, Hernandez-Lucas I, Hong A, Huizar L, Hyman RW, Jones T, Kahn D, Kahn ML, Kalman S, Keating DH, Kiss E, Komp C, Lelaure V, Masuy D, Palm C, Peck MC, Pohl TM, Portetelle D, Purnelle B, Ramsperger U, Surzycki R, Thébault P, Vandenbol M, Vorhölter F-J, Weidner S, Wells DH, Wong K, Yeh K-C, Batut J. 2001. The composite genome of the legume symbiont Sinorhizobium meliloti. Science 293:668–672. https://doi.org/10.1126/science.1060966

Garcillán-Barcia MP, Redondo-Salvo S, de la Cruz F. 2023. Plasmid classifications. Plasmid 126:102684. https://doi.org/10.1016/j.plasmid.2023.102684

Gomis-Rüth FX, Solà M, Acebo P, Párraga A, Guasch A, Eritja R, González A, Espinosa M, del Solar G, Coll M. 1998. The structure of plasmid-encoded transcriptional repressor CopG unliganded and bound to its operator. EMBO J 17:7404–7415. https://doi.org/10.1093/emboj/17.24.7404

González-Montes L, del Campo I, Garcillán-Barcia MP, de la Cruz F, Moncalián G. 2020. ArdC, a ssDNA-binding protein with a metalloprotease domain, overpasses the recipient hsdRMS restriction system broadening conjugation host range. PLoS Genet 16:e1008750. https://doi.org/10.1371/journal.pgen.1008750

Gurevich A, Saveliev V, Vyahhi N, Tesler G. 2013. QUAST: quality assessment tool for genome assemblies. Bioinformatics 29:1072–1075. https://doi.org/10.1093/bioinformatics/btt086

Hall JPJ, Botelho J, Cazares A, Baltrus DA. 2021. What makes a megaplasmid? Philos Trans R Soc B Biol Sci 377:20200472. https://doi.org/10.1098/rstb.2020.0472

Harmer CJ, Moran RA, Hall RM. 2014. Movement of IS26-associated antibiotic resistance genes occurs via a translocatable unit that includes a single IS26 and preferentially inserts adjacent to another IS26. mBio 5:e01801-14. https://doi.org/10.1128/mbio.01801-14

Harrison E, Brockhurst MA. 2012. Plasmid-mediated horizontal gene transfer is a coevolutionary process. Trends Microbiol 20:262–267. https://doi.org/10.1016/j.tim.2012.04.003

Hawes MC, Curlango-Rivera G, Wen F, White GJ, VanEtten HD, Xiong Z. 2011. Extracellular DNA: the tip of root defenses? Plant Sci 180:741–745. https://doi.org/10.1016/j.plantsci.2011.02.007

He S, David S, Rattle J, Sanchez-Garrido J, Low WW, Wong JLC, Beis K, Frankel G. 2026. TraN variants mediate conjugation species specificity of IncA/C, IncH, and Acinetobacter baumannii plasmids. J Bacteriol 208:e00536-25. https://doi.org/10.1128/jb.00536-25

Hua X, Zhang L, Moran RA, Xu Q, Sun L, van Schaik W, Yu Y. 2020. Cointegration as a mechanism for the evolution of a KPC-producing multidrug resistance plasmid in Proteus mirabilis. Emerg Microbes Infect 9:1206–1218. https://doi.org/10.1080/22221751.2020.1773322

Iacovelli R, Bovenberg RAL, Driessen AJM. 2021. Nonribosomal peptide synthetases and their biotechnological potential in Penicillium rubens. J Ind Microbiol Biotechnol 48:kuab045. https://doi.org/10.1093/jimb/kuab045

Ingmer H, Cohen SN. 1993. Excess intracellular concentration of the pSC101 RepA protein interferes with both plasmid DNA replication and partitioning. J Bacteriol 175:7834–7841. https://doi.org/10.1128/jb.175.24.7834-7841.1993

Ipoutcha T, Wang Y, Rocha EPC, Penadés JR. 2026. Mobile genetic elements drive a fusion-deletion life cycle that shapes plasmid evolution and antimicrobial resistance. openRxiv. (preprint) https://doi.org/10.64898/2026.01.09.696371

Jain R, Rivera MC, Moore JE, Lake JA. 2003. Horizontal gene transfer accelerates genome innovation and evolution. Mol Biol Evol 20:1598–1602. https://doi.org/10.1093/molbev/msg154

Jain C, Rodriguez-R LM, Phillippy AM, Konstantinidis KT, Aluru S. 2018. High throughput ANI analysis of 90K prokaryotic genomes reveals clear species boundaries. Nat Commun 9:5114. https://doi.org/10.1038/s41467-018-07641-9

Jeon H, Choi E, Hwang J. 2021. Identification and characterization of VapBC toxin-antitoxin system in Bosea sp. PAMC 26642 isolated from Arctic lichens. RNA 27:1374–1389. https://doi.org/10.1261/rna.078786.121

Katz L, Griswold T, Morrison S, Caravas J, Zhang S, den Bakker H, Deng X, Carleton H. 2019. Mashtree: a rapid comparison of whole genome sequence files. J Open Source Softw 4:1762. https://doi.org/10.21105/joss.01762

Kearsley JVS, Sather LM, Finan TM. 2024. Sinorhizobium (Ensifer) meliloti. Trends Microbiol 32:516–518. https://www.cell.com/trends/microbiology/abstract/S0966-842X(24)00070-2

Kearsley JVS, Geddes BA, diCenzo GC, Zamani M, Finan TM. 2025. A minimized symbiotic gene set from the 1.68 Mb pSymB chromid of Sinorhizobium meliloti reveals auxiliary symbiotic loci. BMC Biol 23:75. https://doi.org/10.1186/s12915-025-02298-5

Kim D, Park S, Chun J. 2021. Introducing EzAAI: a pipeline for high throughput calculations of prokaryotic average amino acid identity. J Microbiol 59:476–480. https://doi.org/10.1007/s12275-021-1154-0

Kolmogorov M, Yuan J, Lin Y, Pevzner PA. 2019. Assembly of long, error-prone reads using repeat graphs. Nat Biotechnol 37:540–546. https://doi.org/10.1038/s41587-019-0072-8

Kosier B, Pühler A, Simon R. 1993. Monitoring the diversity of Rhizobium meliloti field and microcosm isolates with a novel rapid genotyping method using insertion elements. Mol Ecol 2:35–46. https://doi.org/10.1111/j.1365-294X.1993.tb00097.x

Kudryavtseva AA, Cséfalvay E, Gnuchikh EY, Yanovskaya DD, Skutel MA, Isaev AB, Bazhenov SV, Utkina AA, Manukhov IV. 2023. Broadness and specificity: ArdB, ArdA, and Ocr against various restriction-modification systems. Front Microbiol 14:1133144. https://doi.org/10.3389/fmicb.2023.1133144

Kusano K, Naito T, Handa N, Kobayashi I. 1995. Restriction-modification systems as genomic parasites in competition for specific sequences. Proc Natl Acad Sci U S A 92:11095–11099. https://doi.org/10.1073/pnas.92.24.11095

Lagares A, Sanjuán J, Pistorio M. 2014. The plasmid mobilome of the model plant-symbiont Sinorhizobium meliloti: coming up with new questions and answers. Microbiol Spectr 2:PLAS-0005-2013. https://doi.org/10.1128/microbiolspec.plas-0005-2013

Li H. 2018. Minimap2: pairwise alignment for nucleotide sequences. Bioinformatics 34:3094–3100. https://doi.org/10.1093/bioinformatics/bty191

Liao Q, Ren Z, Wiesler EE, Fuqua C, Wang X. 2022. A dicentric bacterial chromosome requires XerC/D site-specific recombinases for resolution. Curr Biol 32:3609–3618.e7. https://doi.org/10.1016/j.cub.2022.06.050

Liao C, Mao F, Qian M, Wang X. 2022. Pathogen-derived nucleases: an effective weapon for escaping extracellular traps. Front Immunol 13:899890. https://doi.org/10.3389/fimmu.2022.899890

Liu Z, Tang Y, He M, Xu C. 2025. Molecular drivers of fusion plasmid: mechanistic insights and evolutionary implications. J Antimicrob Chemother 80:2902–2911. https://doi.org/10.1093/jac/dkaf309

Low WW, Wong JLC, Beltran LC, Seddon C, David S, Kwong H-S, Bizeau T, Wang F, Peña A, Costa TRD, Pham B, Chen M, Egelman EH, Beis K, Frankel G. 2022. Mating pair stabilization mediates bacterial conjugation species specificity. Nat Microbiol 7:1016–1027. https://doi.org/10.1038/s41564-022-01146-4

Luchetti A, Castellani LG, Toscani AM, Lagares A, Del Papa MF, Torres Tejerizo G, Pistorio M. 2023. Characterization of an accessory plasmid of Sinorhizobium meliloti and its two replication-modules. PLoS ONE 18:e0285505. https://doi.org/10.1371/journal.pone.0285505

Maillet F, Fournier J, Mendis HC, Tadege M, Wen J, Ratet P, Mysore KS, Gough C, Jones KM. 2020. Sinorhizobium meliloti succinylated high-molecular-weight succinoglycan and the Medicago truncatula LysM receptor-like kinase MtLYK10 participate independently in symbiotic infection. Plant J 102:311–326. https://doi.org/10.1111/tpj.14625

McInnes L, Healy J, Astels S. 2017. hdbscan: hierarchical density based clustering. J Open Source Softw 2:205. https://doi.org/10.21105/joss.00205

McInnes L, Healy J, Saul N, Großberger L. 2018. UMAP: uniform manifold approximation and projection. J Open Source Softw 3:861. https://doi.org/10.21105/joss.00861

Mercado-Blanco J, Olivares J. 1993. Stability and transmissibility of the cryptic plasmids of Rhizobium meliloti GR4. Arch Microbiol 160:477–485. https://doi.org/10.1007/BF00245309

Mercado-Blanco J, Toro N. 1996. Plasmids in rhizobia: the role of nonsymbiotic plasmids. Mol Plant-Microbe Interact 9:535–545. https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf

Molano L-AG, Hirsch P, Hannig M, Müller R, Keller A. 2024. The PLSDB 2025 update: enhanced annotations and improved functionality for comprehensive plasmid research. Nucleic Acids Res 53:D189–D196. https://doi.org/10.1093/nar/gkae1095

Mori JF, Kanaly RA. 2022. Natural chromosome-chromid fusion across rRNA operons in a Burkholderiaceae bacterium. Microbiol Spectr 10:e02225-21. https://doi.org/10.1128/spectrum.02225-21

Murphy AC, Corney M, Monson RE, Matilla MA, Salmond GPC, Leeper FJ. 2023. Biosynthesis of antifungal solanimycin may involve an iterative nonribosomal peptide synthetase module. ACS Chem Biol 18:1148–1157. https://doi.org/10.1021/acschembio.2c00947

Ni S, Li B, Tang K, Yao J, Wood TK, Wang P, Wang X. 2021. Conjugative plasmid-encoded toxin-antitoxin system PrpT/PrpA directly controls plasmid copy number. Proc Natl Acad Sci U S A 118:e2011577118. https://doi.org/10.1073/pnas.2011577118

Ondov BD, Treangen TJ, Melsted P, Mallonee AB, Bergman NH, Koren S, Phillippy AM. 2016. Mash: fast genome and metagenome distance estimation using MinHash. Genome Biol 17:132. https://doi.org/10.1186/s13059-016-0997-x

Oxford Nanopore Technologies. Medaka: sequence correction provided by ONT Research. Oxford Nanopore Technologies, Oxford, UK. https://github.com/nanoporetech/medaka

Orlek A, Stoesser N, Anjum MF, Doumith M, Ellington MJ, Peto T, Crook D, Woodford N, Walker AS, Phan H, Sheppard AE. 2017. Plasmid classification in an era of whole-genome sequencing: application in studies of antibiotic resistance epidemiology. Front Microbiol 8:182. https://doi.org/10.3389/fmicb.2017.00182

Park H-J, Wang W, Curlango-Rivera G, Xiong Z, Lin Z, Huskey DA, Hawes MC, VanEtten HD, Turgeon BG. 2019. A DNase from a fungal phytopathogen is a virulence factor likely deployed as counter defense against host-secreted extracellular DNA. mBio 10:e02805-18. https://doi.org/10.1128/mbio.02805-18

Parks DH, Imelfort M, Skennerton CT, Hugenholtz P, Tyson GW. 2015. CheckM: assessing the quality of microbial genomes recovered from isolates, single cells, and metagenomes. Genome Res 25:1043–1055. https://doi.org/10.1101/gr.186072.114

Passeri I, Cangioli L, Fondi M, Mengoni A, Fagorzi C. 2025. The complex epigenetic panorama in the multipartite genome of the nitrogen-fixing bacterium Sinorhizobium meliloti. Genome Biol Evol 17:evae245. https://doi.org/10.1093/gbe/evae245

Patel SJ, Padilla-Benavides T, Collins JM, Argüello JM. 2014. Functional diversity of five homologous Cu+-ATPases present in Sinorhizobium meliloti. Microbiology (Reading) 160:1237–1251. https://doi.org/10.1099/mic.0.079137-0

Pedregosa F, Varoquaux G, Gramfort A, Michel V, Thirion B, Grisel O, Blondel M, Prettenhofer P, Weiss R, Dubourg V, Vanderplas J, Passos A, Cournapeau D, Brucher M, Perrot M, Duchesnay É. 2011. Scikit-learn: machine learning in Python. J Mach Learn Res 12:2825–2830. https://www.jmlr.org/papers/v12/pedregosa11a.html

Pérez-Oseguera Á, Cevallos MA. 2013. RepA and RepB exert plasmid incompatibility repressing the transcription of the repABC operon. Plasmid 70:362–376. https://doi.org/10.1016/j.plasmid.2013.08.001

Pesesky MW, Tilley R, Beck DAC. 2019. Mosaic plasmids are abundant and unevenly distributed across prokaryotic taxa. Plasmid 102:10–18. https://doi.org/10.1016/j.plasmid.2019.02.003

Pfeifer E, Rocha EPC. 2024. Phage-plasmids promote recombination and emergence of phages and plasmids. Nat Commun 15:1545. https://doi.org/10.1038/s41467-024-45757-3

Pistorio M, Del Papa MF, Balagué LJ, Lagares A. 2003. Identification of a transmissible plasmid from an Argentine Sinorhizobium meliloti strain which can be mobilised by conjugative helper functions of the European strain S. meliloti GR4. FEMS Microbiol Lett 225:15–21. https://doi.org/10.1016/S0378-1097(03)00454-3

Pistorio M, Giusti MA, Del Papa MF, Draghi WO, Lozano MJ, Torres Tejerizo G, Lagares A. 2008. Conjugal properties of the Sinorhizobium meliloti plasmid mobilome. FEMS Microbiol Ecol 65:372–382. https://doi.org/10.1111/j.1574-6941.2008.00509.x

Qian W, Zhang J. 2014. Genomic evidence for adaptation by gene duplication. Genome Res 24:1356–1362. https://doi.org/10.1101/gr.172098.114

Qu D, Shen Y, Hu L, Jiang X, Yin Z, Gao B, Zhao Y, Yang W, Yang H, Han J, Zhou D. 2019. Comparative analysis of KPC-2-encoding chimera plasmids with multi-replicon IncR:IncpA1763-KPC:IncN1 or IncFIIpHN7A8:IncpA1763-KPC:IncN1. Infect Drug Resist 12:285–296. https://doi.org/10.2147/IDR.S189168

Ranjan A, Rajput VD, Prazdnova EV, Gurnani M, Bhardwaj P, Sharma S, Sushkova S, Mandzhieva SS, Minkina T, Sudan J, Zargar SM, Chauhan A, Jindal T. 2023. Nature's antimicrobial arsenal: non-ribosomal peptides from PGPB for plant pathogen biocontrol. Fermentation 9:597. https://doi.org/10.3390/fermentation9070597

Redondo-Salvo S, Fernández-López R, Ruiz R, Vielva L, de Toro M, Rocha EPC, Garcillán-Barcia MP, de la Cruz F. 2020. Pathways for horizontal gene transfer in bacteria revealed by a global map of their plasmids. Nat Commun 11:3602. https://doi.org/10.1038/s41467-020-17278-2

Rehm N, Buchinger S, Strösser J, Dotzauer A, Walter B, Hans S, Bathe B, Schomburg D, Krämer R, Burkovski A. 2010. Impact of adenylyltransferase GlnE on nitrogen starvation response in Corynebacterium glutamicum. J Biotechnol 145:244–252. https://doi.org/10.1016/j.jbiotec.2009.11.024

Riley AB, Grillo MA, Epstein B, Tiffin P, Heath KD. 2022. Discordant population structure among rhizobium divided genomes and their legume hosts. Mol Ecol 32:2646–2659. https://doi.org/10.1111/mec.16704

Robertson J, Nash JHE. 2018. MOB-suite: software tools for clustering, reconstruction and typing of plasmids from draft assemblies. Microb Genom 4:e000206. https://doi.org/10.1099/mgen.0.000206

Roumiantseva ML, Andronov EE, Sharypova LA, Dammann-Kalinowski T, Keller M, Young JPW, Simarov BV. 2002. Diversity of Sinorhizobium meliloti from the central Asian alfalfa gene center. Appl Environ Microbiol 68:4694–4697. https://doi.org/10.1128/AEM.68.9.4694-4697.2002

Sanjuan J, Olivares J. 1989. Implication of nifA in regulation of genes located on a Rhizobium meliloti cryptic plasmid that affect nodulation efficiency. J Bacteriol 171:4154–4161. https://doi.org/10.1128/jb.171.8.4154-4161.1989

Schalk IJ. 2024. Bacterial siderophores: diversity, uptake pathways and applications. Nat Rev Microbiol 23:24–40. https://doi.org/10.1038/s41579-024-01090-6

Schlaman HRM, Phillips DA, Kondorosi E. 1998. Genetic organization and transcriptional regulation of rhizobial nodulation genes, p 361–386. In The Rhizobiaceae. Springer, Dordrecht. https://doi.org/10.1007/978-94-011-5060-6_19

Schwengers O, Jelonek L, Dieckmann MA, Beyvers S, Blom J, Goesmann A. 2021. Bakta: rapid and standardized annotation of bacterial genomes via alignment-free sequence identification. Microb Genom 7:000685. https://doi.org/10.1099/mgen.0.000685

scikit-bio development team. scikit-bio: a bioinformatics library for data scientists, students, and developers. https://scikit.bio

Sharma P, Garg N, Sharma A, Capalash N, Singh R. 2019. Nucleases of bacterial pathogens as virulence factors, therapeutic targets and diagnostic markers. Int J Med Microbiol 309:151354. https://doi.org/10.1016/j.ijmm.2019.151354

Shaw LP, Rocha EPC, MacLean RC. 2023. Restriction-modification systems have shaped the evolution and distribution of plasmids across bacteria. Nucleic Acids Res 51:6806–6818. https://doi.org/10.1093/nar/gkad452

Shen W, Sipos B, Zhao L. 2024. SeqKit2: a Swiss army knife for sequence and alignment processing. iMeta 3:e191. https://doi.org/10.1002/imt2.191

Si Y-W, Feng M-D, Yang B-S, Liu Y-N, Liu K-H, Wang Y, Jiao J, Tian C-F. 2025. Evolution of rhizobial siderophore utilization via accessory xeno-siderophore receptors and flexible intake machinery for self-produced siderophores. ISME J 20:wraf280. https://doi.org/10.1093/ismejo/wraf280

Smillie C, Garcillán-Barcia MP, Francia MV, Rocha EPC, de la Cruz F. 2010. Mobility of plasmids. Microbiol Mol Biol Rev 74:434–452. https://doi.org/10.1128/mmbr.00020-10

Stiens M, Schneiker S, Keller M, Kuhn S, Pühler A, Schlüter A. 2006. Sequence analysis of the 144-kilobase accessory plasmid pSmeSM11a, isolated from a dominant Sinorhizobium meliloti strain identified during a long-term field release experiment. Appl Environ Microbiol 72:3662–3672. https://doi.org/10.1128/AEM.72.5.3662-3672.2006

Stiens M, Schneiker S, Pühler A, Schlüter A. 2007. Sequence analysis of the 181-kb accessory plasmid pSmeSM11b, isolated from a dominant Sinorhizobium meliloti strain identified during a long-term field release experiment. FEMS Microbiol Lett 271:297–309. https://doi.org/10.1111/j.1574-6968.2007.00731.x

Szuplewska M, Czarnecki J, Bartosik D. 2015. Autonomous and non-autonomous Tn3-family transposons and their role in the evolution of mobile genetic elements. Mob Genet Elements 4:e998537. https://doi.org/10.1080/2159256X.2014.998537

Taguchi H, Koike-Takeshita A. 2023. In vivo client proteins of the chaperonin GroEL-GroES provide insight into the role of chaperones in protein evolution. Front Mol Biosci 10:1091677. https://doi.org/10.3389/fmolb.2023.1091677

Tesson F, Hervé A, Mordret E, Touchon M, d’Humières C, Cury J, Bernheim A. 2022. Systematic and quantitative view of the antiviral arsenal of prokaryotes. Nat Commun 13:2561. https://doi.org/10.1038/s41467-022-30269-9

Thomas CM, Nielsen KM. 2005. Mechanisms of, and barriers to, horizontal gene transfer between bacteria. Nat Rev Microbiol 3:711–721. https://doi.org/10.1038/nrmicro1234

Tonkin-Hill G, MacAlasdair N, Ruis C, Weimann A, Horesh G, Lees JA, Gladstone RA, Lo S, Beaudoin C, Floto RA, Frost SDW, Corander J, Bentley SD, Parkhill J. 2020. Producing polished prokaryotic pangenomes with the Panaroo pipeline. Genome Biol 21:180. https://doi.org/10.1186/s13059-020-02090-4

Tran TM, MacIntyre A, Hawes M, Allen C. 2016. Escaping underground nets: extracellular DNases degrade plant extracellular traps and contribute to virulence of the plant pathogenic bacterium Ralstonia solanacearum. PLoS Pathog 12:e1005686. https://doi.org/10.1371/journal.ppat.1005686

Vasu K, Nagaraja V. 2013. Diverse functions of restriction-modification systems in addition to cellular defense. Microbiol Mol Biol Rev 77:53–72. https://doi.org/10.1128/mmbr.00044-12

Vereau Gorbitz D, Schwarz CP, McMullen JG, Cerón-Romero M, Doyle RT, Lau JA, Whitaker RJ, Vanderpool CK, Heath KD. 2025. Plasmid transmission dynamics and evolution of partner quality in a natural population of Rhizobium leguminosarum. mBio 16:e02497-25. https://doi.org/10.1128/mbio.02497-25

Virtanen P, Gommers R, Oliphant TE, Haberland M, Reddy T, Cournapeau D, Burovski E, Peterson P, Weckesser W, Bright J, van der Walt SJ, Brett M, Wilson J, Millman KJ, Mayorov N, Nelson ARJ, Jones E, Kern R, Larson E, Carey CJ, Polat İ, Feng Y, Moore EW, VanderPlas J, Laxalde D, Perktold J, Cimrman R, Henriksen I, Quintero EA, Harris CR, Archibald AM, Ribeiro AH, Pedregosa F, van Mulbregt P, SciPy 1.0 Contributors. 2020. SciPy 1.0: fundamental algorithms for scientific computing in Python. Nat Methods 17:261–272. https://doi.org/10.1038/s41592-019-0686-2

Wang P, Guo Q, Jiang X, Lu P, Chang M, Yang L, Li M, Wang C, Xiao T, Xiao Y, Zhu H. 2025. Deciphering gene redundancy in prokaryotic genomes provides evolutionary insights for pathogenicity and its roles in clinical infections. Nat Commun 16:9974. https://doi.org/10.1038/s41467-025-65840-7

Wang X, Zhao J, Ji F, Chang H, Qin J, Zhang C, Hu G, Zhu J, Yang J, Jia Z, Li G, Qin J, Wu B, Wang C. 2021. Multiple-replicon resistance plasmids of Klebsiella mediate extensive dissemination of antimicrobial genes. Front Microbiol 12:754931. https://doi.org/10.3389/fmicb.2021.754931

Wangthaisong P, Piromyou P, Songwattana P, Phimphong T, Songsaeng A, Pruksametanan N, Boonchuen P, Wongdee J, Teamtaisong K, Boonkerd N, Sato S, Tittabutr P, Teaumroong N. 2024. CopG1, a novel transcriptional regulator affecting symbiosis in Bradyrhizobium sp. SUTN9-2. Biology (Basel) 13:415. https://doi.org/10.3390/biology13060415

Wickramarachchi A, Mallawaarachchi V. kmertools: DNA vectorisation tool. https://github.com/anuradhawick/kmertools

Wong K, Finan T, Golding B. 2002. Dinucleotide compositional analysis of Sinorhizobium meliloti using the genome signature: distinguishing chromosomes and plasmids. Funct Integr Genomics 2:274–281. https://doi.org/10.1007/s10142-002-0068-0

Yamamoto S, Kiyokawa K, Tanaka K, Moriguchi K, Suzuki K. 2009. Novel toxin-antitoxin system composed of serine protease and AAA-ATPase homologues determines the high level of stability and incompatibility of the tumor-inducing plasmid pTiC58. J Bacteriol 191:4656–4666. https://doi.org/10.1128/jb.00124-09

Yu MK, Fogarty EC, Eren AM. 2024. Diverse plasmid systems and their ecology across human gut metagenomes revealed by PlasX and MobMess. Nat Microbiol 9:830–847. https://doi.org/10.1038/s41564-024-01610-3
