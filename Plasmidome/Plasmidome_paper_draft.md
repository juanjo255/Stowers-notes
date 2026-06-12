# The Accessory Plasmidome of *Sinorhizobium meliloti*: Diversity, Distribution, and Functional Repertoire

---

> **DRAFT — 2026-06-03**
> **[NEW REF — verify: \<claim\>]** markers = citations added during drafting not present in the original notes. Verify DOIs before submission.
> **⚠️ DISCREPANCY** markers = numeric or factual inconsistencies flagged for author resolution.

---

## Abstract

*Sinorhizobium meliloti* is a soil alphaproteobacterium renowned for its nitrogen-fixing symbiosis with leguminous plants and for carrying one of the most extensively studied multipartite genomes in bacteria. While the two megaplasmids pSymA and pSymB have been intensively characterized, the accessory plasmids of *S. meliloti* remain poorly described. Here, we present a comprehensive survey of the *S. meliloti* accessory plasmidome by combining long-read whole-genome sequencing of 256 strains from three geographically distinct collections with sequences retrieved from public databases. Using a *de novo* k-mer-based identification strategy followed by containment-based de-replication with MobMess, we catalogued 304 unique accessory plasmid sequences

> ⚠️ DISCREPANCY: prose states "304 unique accessory plasmids / 223 new" but the de-replication table totals 303 sequences — please verify.

ranging from 12 kb to 749 kb, of which the majority represent previously undescribed elements. Accessory plasmids were classified into 15 *Sinorhizobium*-specific replicon groups (Si01–Si15) and two shared groups with *Rhizobium leguminosarum* (Rh07 and Rh08), revealing inter-genus plasmid exchange. Functional annotation uncovered diverse gene repertoires including toxin-antitoxin systems, defense mechanisms, biosynthetic gene clusters dominated by non-ribosomal peptide synthetases, and signal peptide-bearing proteins with roles in host interaction. Evidence for recurrent plasmid fusion events mediated by Tn3-family transposases, and the presence of plasmids up to 749 kb that exceed canonical megaplasmid thresholds, point to ongoing genomic dynamism in this lineage. These findings provide the first systematic description of the *S. meliloti* accessory plasmidome and establish a foundation for understanding accessory plasmid function in soil ecology and legume symbiosis.

**Keywords**: *Sinorhizobium meliloti*; accessory plasmids; plasmidome; RepABC; horizontal gene transfer; biosynthetic gene clusters; rhizobia; long-read sequencing

---

## Introduction

*Sinorhizobium meliloti* is a gram-negative alphaproteobacterium from the family *Rhizobiaceae* that fixes atmospheric nitrogen in root nodule symbioses with legumes of the genera *Medicago*, *Melilotus*, and *Trigonella* **[NEW REF — verify: S. meliloti symbiosis host range review]**. The species has long served as a model for bacterial symbiosis, multipartite genome evolution, and soil microbiology. The reference strain Rm1021 carries a 3.65 Mb chromosome, the 1.35 Mb symbiotic megaplasmid pSymA, and the 1.68 Mb megaplasmid pSymB **[NEW REF — verify: Galibert et al. 2001 Science — S. meliloti Rm1021 genome sequence]**. pSymA encodes the majority of nodulation (*nod*) and nitrogen fixation (*nif*, *fix*) genes, whereas pSymB carries genes essential for exopolysaccharide biosynthesis, solute transport, and other functions required for symbiosis and free-living fitness. Notably, pSymB has accumulated chromosome-like features — including a high degree of gene essentiality and codon usage resembling the chromosome — leading to its classification as a "chromid" **[NEW REF — verify: Harrison et al. 2010 Mol Biol Evol — chromid classification framework]**; [diCenzo & Finan (2015)](https://doi.org/10.1007/s00438-015-0998-6). This evolutionary trajectory contrasts with pSymA, which retains more plasmid-like characteristics including higher rates of gene gain and loss [diCenzo & Finan (2015)](https://doi.org/10.1007/s00438-015-0998-6).

*S. meliloti* is recognized as having an open pan-genome, reflected in extensive accessory gene content and remarkable phenotypic diversity within the species [ref 1](https://doi.org/10.1186/1471-2164-12-235), [ref2](https://doi.org/10.1371/journal.pcbi.1004478). Beyond the two megaplasmids, individual strains frequently harbor smaller, so-called "accessory" or "cryptic" plasmids whose biological functions have remained largely obscure [Mercado-Blanco & Toro (1996)](https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf); [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411). Early reports noted that these plasmids could affect competitive fitness during host nodulation [Selbitschka et al. (2006)](https://doi.org/10.1007/s00248-006-9056-6); [Schuleter et. al (2007)](https://doi.org/10.1111/j.1574-6968.2007.00731.x), yet the full scope of their genetic diversity, replication machinery, and functional repertoires has not been systematically assessed.

A fundamental challenge in *S. meliloti* plasmid biology is their classification. Unlike *Enterobacterales* plasmids, for which incompatibility (Inc) typing is well established, the dominant replication system in *Rhizobiaceae* plasmids is the repABC operon — a three-gene cassette largely absent from enterobacterial plasmids and incompatible with the canonical Inc scheme [Cevallos et al. (2008)](https://doi.org/10.1016/j.plasmid.2013.08.001) **[NEW REF — verify: Pinto et al. 2012 — repABC in alphaproteobacteria, check year/journal]**. Recent efforts to extend replicon typing to *Rhizobiales* and to classify plasmids into Plasmid Taxonomic Units (PTUs) by network-based approaches have opened new avenues [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2); [Cavassim et. al (2020)](https://doi.org/10.1099/mgen.0.000351); [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25), but *S. meliloti* accessory plasmids remain under-represented in public databases and have not been the subject of a dedicated plasmidome study.

Here we address this gap by characterizing the accessory plasmidome of *S. meliloti* across 256 strains sequenced with long-read technologies (PacBio HiFi and Oxford Nanopore), supplemented by publicly available sequences from PLSDB. We describe the size, structural organization, and replication machinery of these elements; define species-level replicon groups; and characterize their functional gene content including defense systems, biosynthetic gene clusters, and evidence of inter-plasmid gene exchange. Our results reveal a highly diverse and largely uncharacterized plasmid reservoir in *S. meliloti* and identify recurrent themes of large-plasmid evolution including MGE-mediated fusion events and ecological differentiation of gene content.

---

## Results

### Genome Assembly Quality and Strain Taxonomic Identity

> ⚠️ DISCREPANCY: Methods states "258 strains with PacBio HiFi and 95 with ONT" but this section and the diversity section refer to "256 genomes sequenced." Possible explanation: two assemblies excluded post-QC (the Pseudomonas and Rhizobiales contaminations). Please verify the correct total.

A total of 256 *S. meliloti* genomes were assembled from three long-read sequencing datasets: in-house PacBio HiFi assemblies, PacBio HiFi assemblies from the Penn State collection (Liana), and Oxford Nanopore assemblies from the Dakota collaboration. Genome completeness assessed by CheckM single-copy ortholog markers was consistently high across datasets, with the majority of assemblies exceeding 98% completeness (Figure 1 — `compleness_all_datasets.png`). As expected, PacBio HiFi assemblies achieved greater contiguity than ONT assemblies at comparable coverage; ONT assemblies showed higher fragmentation especially of large replicons at low sequencing depth (Figure 2 — `number_circular_contigs_per_dataset.png`). Coverage distributions indicated that applying a 30× threshold to accessory elements would have eliminated the majority of the data in the Penn State and Dakota collections, whereas applying it only to chromosomal sequences would have removed fewer than 25% of genomes. Accordingly, coverage thresholds were applied selectively by replicon type (Figure 3 — `len_QC_distri_all_datasets.png`).

Contamination assessment identified one assembly classified to *Pseudomonas* (MAG154_2_filtered) and one to *Rhizobiales* (m64404e_240531_162148.hifi_reads.bc2090--bc2090); both were excluded from downstream analyses.

To confirm taxonomic identity, a Mash-distance phylogeny was constructed using 3,308 RefSeq genomes from the family *Rhizobiaceae* (Figure 4 — `tree_rhizobiaceae_w_our_strains.png`). All study strains were placed firmly within the genus *Sinorhizobium*. Pairwise whole-genome ANI calculated with FastANI confirmed that all genomes exceeded 99% ANI with reference *S. meliloti* genomes (Figure 5 — `ANI_strains.png`). As expected from sample origin, the Penn State dataset exhibited the highest within-group similarity, followed by the Dakota dataset, while in-house sequenced strains displayed the broadest spread. Comparative analysis using strain Rm1021 as reference revealed proteome coverage exceeding 78% and average amino acid identity above 98% across all genomes (Figure 6 — `AAI_strains_to_ref.png`), consistent with the known open pan-genome and high accessory gene content of *S. meliloti* [ref 1](https://doi.org/10.1186/1471-2164-12-235), [ref2](https://doi.org/10.1371/journal.pcbi.1004478).

A subset of assemblies contained chromosomes exceeding 4 Mb with only two contigs larger than 1 Mb (Table 1). Dot-plot mapping of P9E10_R3L_R4X assembly against the Rm1021 reference confirmed pSymB-corresponding sequences within the enlarged chromosome contig, suggesting chromosomal integration of pSymB sequences or an assembly artefact requiring further investigation.

**Table 1. Strains with chromosomes >4 Mb and fewer than three contigs >1 Mb.**

| Sample ID | Contigs >1 Mb |
|---|---|
| P9E10_R3L_R4X | 2 |
| P9F10_G8T_R4X | 2 |
| P9F12 | 3 |
| P9G1 | 3 |
| P9G10 | 3 |
| P9G11 | 3 |
| P9G12 | 3 |
| P9G9 | 3 |
| m64404e_240423_150118.hifi_reads.bc2010--bc2010 | 2 |
| m64404e_240423_150118.hifi_reads.bc2013--bc2013 | 3 |
| m64404e_240423_150118.hifi_reads.bc2069--bc2069 | 3 |
| m64404e_240423_150118.hifi_reads.bc2077--bc2077 | 3 |
| m64404e_240423_150118.hifi_reads.bc2084--bc2084 | 3 |
| m64404e_240423_150118.hifi_reads.bc2090--bc2090 | 3 |
| m64404e_240531_162148.hifi_reads.bc2060--bc2060 | 3 |
| m64404e_240531_162148.hifi_reads.bc2074--bc2074 | 3 |
| m64404e_240531_162148.hifi_reads.bc2076--bc2076 | 2 |
| m64404e_240531_162148.hifi_reads.bc2079--bc2079 | 3 |

---

### De Novo Identification of Accessory Plasmid Contigs

Given the high degree of genome fragmentation at low coverage and the limited representation of *S. meliloti* accessory plasmids in public databases, we employed a *de novo* k-mer composition approach to distinguish accessory plasmid contigs from chromosomal and megaplasmid sequences. Bray-Curtis distances computed from 3-mer frequencies were reduced to two dimensions by principal coordinate analysis (PCoA), and KMeans clustering was applied to define sequence-type clusters (Figure 7 — `de_novo_plasmids_contig_identi.png`). This strategy mirrors that of [Wong, Finan & Golding (2002)](https://doi.org/10.1007/s10142-002-0068-0), who used dinucleotide signatures to discern the biology of the pSymB replicon.

The analysis produced a clear separation of sequences corresponding to the chromosome, pSymA, pSymB, and "Other" — the last category encompassing fragmented contigs and putative accessory plasmids. Clusters 2, 3, and 0 corresponded unambiguously to the chromosome, pSymA, and pSymB, respectively. Among the remaining clusters, GC content and length distributions of sequences above 10 kb indicated that cluster 1 contained biologically relevant accessory plasmid sequences, while cluster 4 was retained to capture potentially small plasmids (Figure 8 — `de_novo_len_gc.png`).

---

### Plasmid De-Replication and Dataset Diversity

To integrate sequences from all three in-house datasets with publicly available *S. meliloti*-associated plasmids from PLSDB (2024v2, ≤500 kb) and related sequences identified by MOB-typer mash clustering, we applied MobMess for containment-based de-replication. MobMess identifies "plasmid systems" by modeling containment relationships between sequences, enabling the distinction of complete plasmids from fragments while retaining distributional information. Because sequence similarity between megaplasmids (especially pSymA) and accessory plasmids represents a known source of assembly ambiguity, megaplasmids were included in the MobMess analysis to prevent false-positive assignments (Figure 9 — `mobmess_all_plsdb.png`). MobMess correctly identified fragmentation artefacts: for example, cluster 129 contains 12–15 kb fragments creating assembly ambiguity between pSymA and a group of accessory plasmids (Figure 10 — `cluster129.png`).

We retained backbone clusters (complete or near-complete plasmids), compound clusters (plasmid systems), and maximal clusters in which all members were below 1 Mb and at least one member was circularly assembled. Non-circular sequences were excluded from maximal clusters to reduce ambiguity, as cases such as contig_3_P9H2 and contig_9_P9E8 revealed large contigs connected to megaplasmid sequences via insertion sequences representing assembly artefacts rather than genuine independent plasmids. Fragment clusters were retained for plasmid distribution analyses.

We recovered 33, 125, and 171 accessory plasmid sequences from the in-house, Penn State, and Dakota Nanopore datasets, respectively.

> ⚠️ DISCREPANCY: Prose states "346 plasmids out of the initial 532 sequences" passed initial filtering before de-replication. The sum of in-house + Penn State + Dakota = 33+125+171 = 329, not 532 or 346. The MobMess table totals 303 sequences after clustering. Please clarify: (a) Does 532 include all contigs entering MobMess (including PLSDB sequences)? (b) Does 346 refer to sequences after PLSDB+in-house joint filtering but before de-replication? (c) Are 303/304 the final unique sequences after de-replication?

After de-replication with MobMess, the analysis yielded 101 unique plasmid clusters encompassing 303 total sequences (Table 2). Very few clusters were shared between datasets, suggesting ecological or geographic specificity in plasmid distribution. The Penn State dataset, despite contributing the largest number of sequences, yielded the fewest unique clusters (9), consistent with the high within-collection strain similarity. The in-house dataset, with the greatest strain diversity by ANI, yielded 28 unique clusters from only 33 sequences.

> ⚠️ DISCREPANCY: Prose states "304 unique accessory plasmids" and "223 are new plasmid sequences reported in this study" but the table totals 303 sequences. The "223 new" figure also needs a denominator clarification (223/304, 223/303, or 223 of a subset excluding database plasmids?).

No linear plasmid as defined by [Hawkey et al. (2022)](https://doi.org/10.1099/mgen.0.000807) was found among the assembled strains.

**Table 2. MobMess de-replication summary by dataset.**

| Dataset                                 | Compound | Maximal | Backbone | Total Clusters | Total Sequences |
| --------------------------------------- | -------- | ------- | -------- | -------------- | --------------- |
| [database]                              | 6        | 0       | 2        | 8              | 17              |
| [penn_state]                            | 4        | 2       | 3        | 9              | 134             |
| [dakota_nanopore]                       | 3        | 42      | 6        | 51             | 120             |
| [in_house]                              | 3        | 24      | 1        | 28             | 33              |
| [dakota_nanopore, penn_state]           | 0        | 1       | 0        | 2              | 0               |
| [database, in_house, dakota_nanopore]   | 0        | 1       | 0        | 1              | 0               |
| [database, penn_state, dakota_nanopore] | 0        | 0       | 3        | 3              | 0               |
| **Total**                               | **16**   | **70**  | **15**   | **101**        | **303**         |

For subsequent functional analyses, database-derived plasmids were retained only if classified as backbone or compound clusters, as the PLSDB-derived set includes plasmids from organisms identified by proximity to *S. meliloti* rather than confirmed *S. meliloti* isolates. Database plasmids were included in the gene repertoire relatedness network.

---

### Sequence Identity Landscape of the De-Replicated Plasmids

Pairwise ANI and alignment fraction (AF) were computed for all unique sequences using Vclust. When AF was calculated relative to the maximum length of each pair (Figure 11 — `plot2_kdeplot_ani_vs_af.png`), a dense cluster appeared at AF ~0.3–0.4 with a tail extending toward high ANI and high AF, representing plasmids in near-complete containment relationships consistent with fusion products. When AF was calculated relative to the minimum length (Figure 12 — `plot1_kdeplot_ani_vs_af.png`), the main cluster shifted to high ANI (~85–90%) but very low AF (~0.2), indicating that large plasmids frequently share a small conserved region — likely the replication backbone — embedded in otherwise unique sequence contexts. This pattern would cause classical ANI-threshold clustering approaches to overgroup plasmids, masking ecologically distinct elements and potentially overestimating horizontal gene transfer rates within a cluster.

---

### Size, GC Content, and Structural Features

After de-replication, plasmid GC content ranged from 48 to 65% (Figure 13 — `len_GC_uniq_pls_mobmess.png`; `len_GC_uniq_pls_kdeplotpng.png`) and sizes spanned from 12 kb to 749 kb (Figure 14 — `len_QC_distri_all_datasets_plasmids.png`). The largest element (749 kb) substantially exceeds the conventional megaplasmid threshold (~300 kb) and represents the largest non-pSym replicon reported in this species. Assembly graph inspection confirmed a fully circularized assembly for one of the two strains carrying this element (P9G4), whereas the second instance was a Type I error (a chimeric assembly incorporating pSymA sequence). A group of 12–23 kb sequences with anomalously high GC content (64.8–65.8%) lacking relaxases, replication, or partition systems were excluded from further functional analyses.

Notably, several large accessory plasmids consistently displayed lower sequencing coverage than the chromosome and megaplasmids in the same assemblies. A ~350 kb plasmid (contig_4_m64404e_240531_162148.hifi_reads.bc2049--bc2049) present across multiple in-house strains showed approximately half the chromosomal coverage. Two re-sequenced strains (Liana_052_1_filtered and Liana_056_3_filtered) carrying this plasmid showed chromosomal-level coverage and additionally harbored a second 75 kb accessory plasmid. This coverage reduction may indicate low-copy number maintenance, restriction to a sub-population of cells within the isolate, or incipient plasmid loss, consistent with models positing vertical transmission dominance for large plasmids to preserve plasmid diversity [Sabnis et. al](https://doi.org/10.1016/j.celrep.2025.116456).

---

### MOB, MPF, and RepABC Annotation

MOB-Suite annotation revealed that MOBQ and MOBP were the two dominant relaxase families (Figure 15 — `mob_typing_uniq_pls_mobmess.png`), consistent with previous reports for *Rhizobiaceae* plasmids [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2).

**Table 3. Relaxase type distribution in de-replicated plasmids.**

| Relaxase type(s) | Count | Notes |
|---|---|---|
| MOBQ | 119 | |
| MOBP | 87 | |
| — | 68 | |
| MOBQ, MOBQ | 25 | |
| MOBP, MOBP | 3 | |
| MOBP, MOBQ | 1 | ~400 kb circular |
| MOBP, MOBQ, MOBQ | 1 | ~240 kb circular |
| **Total** | **304** | ⚠️ Table 3 total is 304 but de-replication table totals 303 — verify. |

**Table 4. MPF type distribution.**

| MPF type | Count |
|---|---|
| MPF_T | 219 |
| — | 85 |
| **Total** | **304** |

Two unusual cases with multiple relaxase types warrant attention. A ~400 kb circular plasmid (P9C10) harbored both MOBP and MOBQ, confirmed by assembly graph inspection as a genuine accessory element with pSymA, pSymB, and the accessory plasmid all correctly resolved and well-covered. A ~240 kb circular plasmid (P9E7_R3L_R4X_Y9Q) contained three relaxase domains (MOBP, MOBQ, MOBQ) confirmed at 240× coverage. Both cases likely represent cointegrate products of ancestral plasmids with different MOB types.

Of the 303 retrieved plasmids, 289 carried at least one *repA* gene and 284 contained a complete *repABC* operon. Thirteen sequences lacked an explicit *repABC* operon; 11 carried related partition/replication annotations (ParB/RepB/Spo0J family partition protein, ParA protein), suggesting divergent but functional replication modules. Two sequences (contig_12_P9E8 and contig_19_P9D4) with high similarity to a 9 kb *E. coli* suicide plasmid (MN057686.1) were removed. Contig_4_P9F11, carrying a *repA* duplication, was also removed. One low-quality 129 kb plasmid (contig_1_m64404e_240531_162148.hifi_reads.bc2080--bc2080) was retained with a quality flag as it belongs to a cluster where other members contain complete RepABC and MOB proteins. The final filtered set comprised **304 plasmids** for functional analyses (Figure 16 — `len_GC_uniq_pls_mobmess_filt.png`; `pls_features_stackbar.png`).

Origin of replication (oriV) sequences were predicted by PlasAnn for 225 of the 304 plasmids. PCA of 6-mer composition from predicted oriV sequences revealed markedly greater compositional diversity among accessory plasmids compared to pSymA, pSymB, and the chromosome (Figure 17 — `PCA_6mer_ori.png`). Critically, the 700 kb false-positive sequence (contig_7_m64404e_240531_162148.hifi_reads.bc2049--bc2049) was placed within the pSymA oriV cluster (Figure 18 — `PCA_6mer_ori_cont_highligth.png`), confirming its chimeric origin and validating oriV composition as a contamination detection tool.

---

### Replicon Typing Defines *Sinorhizobium*-Specific Replicon Groups

In soil alphaproteobacteria such as *S. meliloti*, plasmid replication is dominated by the RepABC family, which is absent from the canonical Inc scheme [del Solar et. al (1998)](https://www.ncbi.nlm.nih.gov/pubmed/9618448); [Cevallos et al. (2008)](https://doi.org/10.1016/j.plasmid.2013.08.001); [Orlek A. et al. (2023)](https://doi.org/10.1016/j.plasmid.2023.102684).

*repA* sequences were extracted from the 304 plasmids and clustered using MMseqs2 (≥70% coverage, ≥90% identity), following [Cavassim et. al (2020)](https://doi.org/10.1099/mgen.0.000351) and [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25), with *Rhizobium leguminosarum* Rh group representatives included (Figure 19 — `replicon_groups.png`). Thirty-six plasmid sequences clustered with Rh07 and 52 with Rh08, indicating plasmid exchange between *Rhizobium* and *Sinorhizobium*. The remaining 205 sequences formed 15 novel *Sinorhizobium*-specific clusters designated Si01–Si15 in order of decreasing abundance (Figure 20 — `repl_group_each_strain_heatmap.png`).

---

### Gene Content Shared Between Accessory Plasmids and Core Replicons

A pan-genome was built with PPanGGoLiN (80% coverage and identity) using 172 genomes presenting circularly assembled chromosomes and megaplasmids, together with 204 associated accessory plasmids (Figure 21 — `gene_share_pls_and_chromosomes.png`; `gene_sharing_upset.png`). pSymB shared more gene families with the chromosome than with pSymA or accessory plasmids, consistent with its chromid status [diCenzo & Finan (2015)](https://doi.org/10.1007/s00438-015-0998-6). pSymA shared more gene families with accessory plasmids than with the chromosome, reflecting its plasmid-like character and proposed role as a major gene acquisition hotspot. Unexpectedly, the chromosome shared more gene families with accessory plasmids than pSymA did. While some of this sharing reflects the documented functional redundancy in *S. meliloti* — for example, the five Cu²⁺-ATPase paralogs that are sequence-similar but functionally non-complementary [Patel et al. (2014)](https://doi.org/10.1099/mic.0.079137-0) — the pattern is also consistent with ongoing bi-directional gene transfer between the chromosome and accessory plasmids.

> **TO DO (author)**: Describe the most common gene families shared with the main replicons before submission.

---

### Accessory Plasmids Carry Diverse but Not Abundant Toxin-Antitoxin Systems

Plasmid maintenance in low-copy elements often relies on post-segregational killing via toxin-antitoxin (TA) systems [Effe *et al.* (2025)](https://doi.org/10.1038/s41467-025-62473-8). *S. meliloti* accessory plasmids have been termed "cryptic plasmids" [Mercado-Blanco & Toro (1996)](https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf); [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411). TA systems were annotated using HMM models from TASmania, which offers higher sensitivity than TADB at the cost of a higher false positive rate [Akarsu et al. (2019)](https://doi.org/10.1371/journal.pcbi.1006946).

TA system accumulation decreased with increasing plasmid size (Figure 22 — `TA_type_vs_length.png`; `heatmap_TA_systems_clustered.png`; `heatmap_TA_systems_mean_clustered.png`), replicating the pattern reported by [Bethke *et al.* (2023)](https://doi.org/10.1093/molbev/msae206). This is consistent with the interpretation that larger plasmids offset the fitness cost of TA systems by carrying beneficial accessory genes, a pattern also documented for restriction-modification systems [Shaw *et al.* (2023)](https://doi.org/10.1093/nar/gkad452). The high prevalence of complete RepABC operons in large plasmids suggests that active partition — rather than TA-mediated addiction — is the dominant maintenance mechanism for large *S. meliloti* accessory plasmids, consistent with the finding that partition combined with TA provides the greatest fitness advantage for low-copy extrachromosomal elements [Effe *et al.* (2025)](https://doi.org/10.1038/s41467-025-62473-8).

The most common annotation associated with TA models was RepB, the partition protein of the RepABC operon, reflecting the known proximity of TA systems to the RepABC operon in *Rhizobiaceae* [Yamamoto et al. (2009)](https://doi.org/10.1128/jb.00124-09); [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411) and the functional overlap between RepA and partitioning [Ingmer & Cohen (1993)](https://doi.org/10.1128/jb.175.24.7834-7841.1993). Plasmids carrying multiple RepABC-related annotations more likely reflect plasmid fusion events (see below). The second most frequent annotation was ArdC (anti-restriction protein type C), which protects single-stranded DNA against type II restriction endonucleases during conjugation [Belogurov et al. (2000)](https://doi.org/10.1006/jmbi.1999.3493); [González-Montes et al. (2020)](https://doi.org/10.1371/journal.pgen.1008750). The Type II TA VapC system and the copy-number regulator CopG [Ni *et al.* (2021)](https://doi.org/10.1073/pnas.2011577118) — also recently implicated in *Bradyrhizobium* symbiosis [Wangthaisong et al. (2024)](https://doi.org/10.3390/biology13060415) — were also among the more common elements.

---

### Defense Systems Can Be Acquired by *S. meliloti* Through Accessory Plasmids

The prevalence of ArdC prompted a broader survey of defense systems using DefenseFinder **[NEW REF — verify: DefenseFinder paper — Tesson et al. 2022 Nat Commun]**. Defense systems were distributed unevenly across replicons: pSymA and the chromosome carried the highest burden, with few strains harboring defense systems on pSymB (Figure 23 — `defense_type_MAG_genomes.png`; `defense_type_acc_pls.png`). On core replicons, SoFIC, Gabija (RM), and SanaTA were the most common. On accessory plasmids, Gabija (RM), CBASS, and additional RM systems were most frequent.

Among RM types in accessory plasmids, types I, II, and IV were detected, with type II the most common (13 of ~100 plasmids with any RM system). On the chromosome and megaplasmids, type II RM was similarly the most frequent (78/256 genomes). This contrasts with the prevailing view that *S. meliloti* carries only type I RM [Ferri et al. (2010)](https://doi.org/10.1016/j.plasmid.2010.01.001); [diCenzo et al. (2022)](https://doi.org/10.1128/mSystems.01092-21); [Passeri et al. (2025)](https://doi.org/10.1093/gbe/evae245). Fifteen genomes and two plasmids harbored type IV RM. Type III RM was the rarest overall.

pSymA carries a conserved ArdB–SoFIC module. SoFIC was recently shown to confer phage protection through AMPylation **[NEW REF — verify: Wu et al. 2025 — SoFIC AMPylation and phage defense]**. ArdB protects against type I RM [Kudryavtseva *et al.* (2023)](https://doi.org/10.3389/fmicb.2023.1133144). By contrast, accessory plasmids predominantly carry ArdC (anti-type II RM). This divergence may reflect evolutionary timing: if pSymA was established before type II RM systems spread through *S. meliloti* populations, ArdB would have been sufficient; the subsequent spread of type II RM may explain why more recently acquired accessory plasmids encode ArdC instead. The presence of RM systems on accessory plasmids indicates that *S. meliloti* can acquire novel defense capabilities via HGT, adding complexity to the conjugation dynamics regulated by methylation patterns and regulatory elements [Dohlemann et al. (2016)](https://doi.org/10.1016/j.jbiotec.2016.06.033); [Passeri et al. (2025)](https://doi.org/10.1093/gbe/evae245); [Castellani et al. (2026)](https://doi.org/10.1128/spectrum.03242-25); [Brom et al. (2014)](https://doi.org/10.1007/978-1-4614-9203-0_3).

---

### Gene Content Profiles Indicate Different Ecological Pressures Between Accessory Plasmids

Large accessory plasmids are thought to provide fitness advantages in complex ecological environments [Hall et al. (2022)](https://doi.org/10.1098/rstb.2020.0472), and accessory plasmid carriage has been proposed to improve competitive fitness in *S. meliloti* [Schuleter et. al (2007)](https://doi.org/10.1111/j.1574-6968.2007.00731.x); [Selbitschka et al. (2006)](https://doi.org/10.1007/s00248-006-9056-6). COG categories were assigned with EggNOG-mapper and a normalized COG frequency matrix was subjected to Bray-Curtis PCoA (Figure 24 — `COGs_feq_matrix_pcoa.png`; `COG_enrich_unq_pls.png`; `COG_plasmids.png`). Plasmid gene functions overlapped across datasets and were not constrained by replicon group identity, consistent with previous reports that replicon and MOB typing have poor resolution for predicting gene content [Douarre et. al (2020)](https://doi.org/10.3389/fmicb.2020.00483); [Orlek at. al (2017)](https://doi.org/10.3389/fmicb.2017.00182); [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2). After HDBSCAN clustering and Fisher exact test with Benjamini-Hochberg correction, significant differences were restricted to Defense mechanisms, Nucleotide transport and metabolism, and Cell motility.

Given the high proportion of hypothetical proteins, this analysis was complemented with a plasmid pan-genome computed by Panaroo (70% initial clustering threshold; 90% identity and coverage). Pairwise dissimilarity matrices were visualized by MDS (Figure 25 — `gene_content_pls_MDS_panaroo.png`), revealing that plasmid clustering was not restricted to individual datasets, clear intra-dataset heterogeneity existed (most notably in the Penn State collection), and a stress value of 0.36 indicated that two-dimensional representation does not fully capture these distance relationships.

Structural variation analysis using Panaroo's gene-triplet framework followed by HDBSCAN and Fisher exact test identified plasmid clusters with distinct genomic arrangements (Figure 26 — `SV_MDS_uniq_pls.png`). Clusters of interest:

- **Cluster 1**: Dienelactone hydrolase-related enzyme and RcgA family transmembrane protein (a conjugation factor in *Rhizobium favelukesii* [Castellani et al. (2026)](https://doi.org/10.1128/spectrum.03242-25)).
- **Cluster 11**: MFS transporter, pyridoxal phosphate-dependent aminotransferase, and SDR family oxidoreductase — consistent with amino acid catabolism.
- **Cluster 13**: MucR family transcriptional regulators and CorA magnesium/cobalt transporter. MucR is a master regulator of quorum sensing and symbiosis in *S. meliloti* **[NEW REF — verify: MucR function in S. meliloti]**, suggesting these plasmids may modulate symbiotic regulatory networks.
- **Cluster 15**: LysR transcriptional regulator, MFS transporter, and PLP-dependent aminotransferase.
- **Cluster 16**: Copper-responsive regulators (CopZ, Cu(I)-responsive regulator), RND-family copper/silver efflux transporter, and periplasmic heavy metal sensor — consistent with heavy metal resistance, relevant for metal-contaminated soils **[NEW REF — verify: heavy metal resistance on Rhizobiaceae plasmids]**.

---

### MGE-Mediated Cointegrate Formation Generates Large Accessory Plasmids in *S. meliloti*

The rightward-skewed size distribution of *S. meliloti* accessory plasmids, combined with the high prevalence of multiple RepABC copies within single plasmids, is consistent with recurrent plasmid fusion events. MGE-mediated cointegrate formation has been proposed as a mechanism driving large-plasmid emergence in clinical settings [Wang et al. (2021)](https://doi.org/10.3389/fmicb.2021.754931); [Liu et al. (2025)](https://doi.org/10.1093/jac/dkaf309); [Penadez et. al (2026)](https://doi.org/10.64898/2026.01.09.696371); [Ipoutcha et al. (2026)](https://doi.org/10.64898/2026.01.09.696371). Plasmid sizes in extensively sequenced bacterial species have been reported to follow bimodal distributions attributed to the distinction between small non-mobilizable and large conjugative plasmids [de la cruz et al. (2010)](https://doi.org/10.1128/mmbr.00020-10); the *S. meliloti* plasmidome lacks this bimodal pattern, with most plasmids concentrated above 60 kb.

Inspection of RepABC copy numbers per plasmid revealed that most accessory plasmids carry multiple RepABC module proteins (Figure 27 — `num_repABC_per_pls_plasAnn.png`; `num_repABC_per_pls.png`). MobMess containment networks provided direct evidence for specific fusion events. A ~314 kb plasmid (contig_4_m64404e_240531_162148.hifi_reads.bc2042--bc2042) corresponds to the fusion of two plasmids (~158 kb and ~146 kb) mediated by a Tn3-family transposase (Figure 28 — `pls_fusion_example.png`). A ~149 kb plasmid (contig_3_m64404e_240423_150118.hifi_reads.bc2012--bc2012) contains an ~73 kb internal plasmid flanked by a Tn3-family transposase (Figure 29 — `pls_fusion_2.png`). Tn3-family transposons are among the mobile elements most strongly associated with cointegrate formation [Szuplewska et al. (2014)](https://doi.org/10.1080/2159256X.2014.998537). Analysis of IS composition per plasmid cluster revealed significant enrichment of specific IS families in distinct accessory plasmid clusters (Figure 30 — `IS_comp_per_cluster.png`; `IS_comp_per_pls.png`).

---

### Accessory Plasmids Are Enriched in Non-Ribosomal Peptide Synthetases

AntiSMASH **[NEW REF — verify: current antiSMASH version and citation]** predicted biosynthetic gene clusters (BGCs) on 194 of the accessory plasmids. NRPS, NI-siderophores, terpenes, and homoserine lactones were the most frequent BGC types (Figure 31 — `antismash_pred_type_frequency.png`; `antismash_pred_type_freq_genome.png`). Unlike the chromosome and megaplasmids, NRPS is the predominant BGC category in accessory plasmids. The most frequently detected NRPS was homologous to Solanimycin non-ribosomal peptide synthetase SolG; Solanimycin is an antifungal compound **[NEW REF — verify: Solanimycin characterization paper — identify producing organism]**, suggesting accessory plasmids may equip *S. meliloti* strains with antifungal capabilities relevant for rhizosphere competition. NI-siderophores mediate scavenging of insoluble ferric iron [Schalk et al. (2025)](https://doi.org/10.1038/s41579-024-01090-6); [Si et al. (2025)](https://doi.org/10.1093/ismejo/wraf280), an important trait under alkaline and neutral soil pH conditions where iron bioavailability is limited. Non-ribosomal peptides have broad applications in antimicrobial biocontrol [lacovelli et al. (2021)](https://doi.org/10.1093/jimb/kuab045); [Fira et al. (2018)](https://doi.org/10.1016/j.jbiotec.2018.07.044); [Ranjan et al. (2023)](https://doi.org/10.3390/fermentation9070597), and their plasmid-mediated distribution raises the possibility that NRPS gene clusters can be horizontally transferred between *S. meliloti* strains.

---

### Accessory Plasmids Carry Signal Peptide-Bearing Proteins With Roles in Host Interaction

A total of 229 accessory plasmids encoded proteins shorter than 200 amino acids with signal peptides identified by SignalP 6.0. The 20 most abundant pan-genome families included substrate-binding proteins linked to transport, nuclease-like proteins associated with evasion of extracellular DNA traps [Sharma et al. (2019)](https://doi.org/10.1016/j.ijmm.2019.151354); [Liag et al. (2022)](https://doi.org/10.3389/fimmu.2022.899890); [Tran et al. (2016)](https://doi.org/10.1371/journal.ppat.1005686); [Park et al. (2019)](https://doi.org/10.1128/mbio.02805-18); [Hawes et al. (2011)](https://doi.org/10.1016/j.plantsci.2011.02.007), and lipoproteins (Figure 32 — `protfams_w_signalp_uniq_pls.png`). The succinoglycan biosynthesis protein ExoI — required for functional nodule formation [Maillet et al. (2019)](https://doi.org/10.1111/tpj.14625) — was identified in the top 20, as was a homolog of LppA, deletion of which reduces exopolysaccharide-I production and competitive fitness during host colonization [Bustamante et al. (2023)](https://doi.org/10.1371/journal.pgen.1010776). The presence of symbiosis-relevant lipoproteins on accessory plasmids suggests these elements can directly contribute to competitive nodulation ability.

---

### Horizontal Gene Transfer Connects *S. meliloti* Accessory Plasmids to the Broader *Rhizobiales* Plasmid Network

All PLSDB sequences (≤500 kb) sharing at least 500 bp with our plasmid set were retrieved using Minimap2 (Figure 33 — `num_pls_per_genus_lt500kb.png`; `Len_pls_lt500kb_per_genus.png`). Weighted Gene Repertoire Relatedness (wGRR) was calculated for all pairs following [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3). Pairs with 0.01 < wGRR < 0.1 were used for network visualization (Figure 34 — `HGT_net_FR_layout.png`; `HGT_net_FR_layout_by_dataset.png`; `pie_genus_connections_uniq_pls.png`).

The vast majority of HGT connections were to plasmids from other *Rhizobiales* / *Hyphomicrobiales*, with 7 of the top 10 most-connected genera belonging to *Rhizobiaceae*. This strong family-level and genus-level restriction is consistent with experimental and bioinformatic evidence that conjugative plasmid transfer in *Rhizobiaceae* is host-lineage-biased, constrained by host defense systems [Dimitriu et al. (2019)](https://doi.org/10.1098/rspb.2019.1110) and molecular specificity of conjugative pilus-receptor interactions [He et al. (2026)](https://doi.org/10.1128/jb.00536-25); [Low et. al (2022)](https://doi.org/10.1038/s41564-022-01146-4).

---

## Discussion

The accessory plasmidome of *S. meliloti* has remained largely uncharacterized despite decades of research on its two megaplasmids. By applying long-read sequencing to 256 strains and combining containment-based de-replication with broad functional annotation, we provide the first systematic description of this plasmid reservoir. Three themes emerge.

**Large size as a defining characteristic.** *S. meliloti* accessory plasmids are unusually large, with a rightward-skewed size distribution concentrated above 60 kb. The prevalence of multiple RepABC modules per plasmid, specific Tn3-mediated fusion events, and IS family enrichment per plasmid cluster collectively argue that cointegrate formation is a recurring process. The largest element (749 kb) approaches the size of small chromids and may represent a transitional state in the trajectory from accessory plasmid to megaplasmid — a trajectory the *S. meliloti* system appears to facilitate through successive fusion events. The combination of low-copy number maintenance (inferred from reduced sequencing coverage), active partition systems (high prevalence of complete RepABC operons), and size-dependent reduction in TA system accumulation are consistent with the theoretical framework for megaplasmid emergence from large accessory elements [Hall *et al.* (2022)](https://doi.org/10.1098/rstb.2020.0472).

**Functional specialization and ecological differentiation.** Gene content analysis revealed that accessory plasmid clusters carry functionally distinct repertoires not predicted by replicon type or collection origin. The enrichment of NRPS-type BGCs (particularly solanimycin-like gene clusters), heavy metal resistance operons (cluster 16), MucR-associated regulators (cluster 13), and diverse transport genes in distinct plasmid clusters suggests that *S. meliloti* uses accessory plasmids to expand its adaptive capacity across heterogeneous soil environments. The presence of symbiosis-relevant lipoproteins (ExoI, LppA homologs) on accessory plasmids raises the possibility that accessory elements contribute to competitive nodulation ability beyond the canonical pSymA-encoded pathway.

**Plasmid mobility and host restriction.** The co-evolutionary dynamics between ArdB (pSymA, anti-type I RM) and ArdC (accessory plasmids, anti-type II RM), combined with the unexpected prevalence of type II RM systems across *S. meliloti* strains, point to a plasmid community shaped by tension between horizontal spread and host restriction. The strong family-level restriction of HGT events to *Rhizobiaceae*, and the 88 plasmids sharing replicon groups with *R. leguminosarum*, together indicate that inter-genus transfer occurs at a lower but non-negligible frequency. The finding that a subset of accessory plasmids carries complete conjugation machinery (MPF_T plus MOB proteins) alongside anti-RM proteins and diverse cargo genes positions them as fully autonomous mobile elements capable of driving inter-cellular transfer.

Several observations warrant follow-up: the biological activity of Solanimycin-like NRPS clusters on accessory plasmids, the functional significance of MucR-family regulators in plasmid-encoded contexts, the mechanisms maintaining large plasmids at sub-chromosomal copy numbers, and the possibility of plasmid-mediated transfer of symbiotic genes between strains in field conditions. From a methodological perspective, the incomplete assembly of some large plasmids due to IS-mediated sequence ambiguity with megaplasmids calls for improved graph-based computational approaches that can resolve these ambiguities using coverage and IS element size as discriminating signals.

---

## Methods

### Genome Assembly and Polishing

> ⚠️ DISCREPANCY: verify "258 PacBio HiFi + 95 ONT" against final count of 256 genomes used downstream.

PacBio HiFi reads were quality-filtered using fastp-long v0.4.1 with default parameters. PacBio HiFi and Oxford Nanopore (ONT) reads were assembled with Flye v2.9.6-b1802 using flags `--pacbio-hifi` and `--nano-hq`, respectively. ONT assemblies were polished with `medaka_consensus` from Medaka v2.1.1 using model `r1041_e82_400bps_sup_v5.2.0`. Assembly quality was assessed with QUAST v5.3.0 and genome completeness estimated with CheckM using the *Ensifer* (UID3566) marker set.

### Taxonomic Confirmation

Whole-genome ANI was calculated with FastANI v1.34. Amino acid identity (AAI) was assessed with EzAAI using strain Rm1021 as the reference. A Mash-distance phylogeny incorporating 3,308 *Rhizobiaceae* RefSeq genomes was built with Mashtree v1.4.6.

### Genome Annotation

All assemblies were annotated with BAKTA v1.11.4. Plasmid sequences were additionally annotated with PlasAnn v1.1.6 for plasmid-specific features (RepABC operons, MOB proteins, oriV prediction).

### De Novo Accessory Plasmid Identification

Bray-Curtis distances were computed from 3-mer frequency profiles of all assembled contigs using `pdist` from SciPy. Dimensionality reduction was performed by PCoA and clusters assigned by KMeans (scikit-learn). GC content and length distributions of sequences above 10 kb were used to validate clusters as biologically informative.

### Plasmid De-Replication

Accessory plasmid sequences from all three in-house datasets were combined with *S. meliloti*-related plasmids from PLSDB 2024v2 (≤500 kb), retrieved by keyword search ("*meliloti*") and confirmed by MOB-typer mash clustering. De-replication used MobMess with megaplasmids retained to prevent false-positive fragmentation artefacts. Backbone, compound, and maximal clusters (≥1 circular member <1 Mb) were retained; non-circular sequences were excluded from maximal clusters.

### MOB and MPF Typing

Relaxase (MOB) and mate pair formation (MPF) types were assigned using MOB-Suite.

### Replicon Typing

*repA* sequences were extracted from all plasmids and clustered with MMseqs2 (≥70% coverage, ≥90% identity). Representative sequences from *R. leguminosarum* Rh groups [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25) were included. Clusters not matching existing Rh groups were designated Si01–Si15 by decreasing abundance.

### Pan-Genome and Gene Content Analysis

Pan-genomes for the core replicons and accessory plasmids were built with PPanGGoLiN (80% coverage and identity) and Panaroo (70% initial clustering threshold, 90% identity/coverage for final grouping), respectively. COG categories were assigned with EggNOG-mapper. Bray-Curtis distance matrices from normalized COG frequencies were visualized by PCoA. Plasmid pan-genome dissimilarity matrices were visualized by MDS. Structural variation clusters were identified with HDBSCAN on Jaccard distance matrices and tested with Fisher's exact test (Benjamini-Hochberg correction).

### Toxin-Antitoxin Systems

TA systems were annotated using HMM models from TASmania.

### Defense Systems

Defense systems were annotated using DefenseFinder **[NEW REF — verify: DefenseFinder paper — Tesson et al. 2022 Nat Commun]**.

### Signal Peptide Prediction

Signal peptides were predicted with SignalP 6.0. Proteins ≤200 aa with signal peptides were assigned to pan-genome families from the PPanGGoLiN analysis.

### Biosynthetic Gene Cluster Prediction

BGCs were predicted using antiSMASH **[NEW REF — verify: current antiSMASH version and citation]**.

### Horizontal Gene Transfer

PLSDB sequences (≤500 kb) were aligned to study plasmids using Minimap2 to retrieve sequences sharing ≥500 bp. Weighted Gene Repertoire Relatedness (wGRR) was calculated following [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3). Pairs with 0.01 < wGRR < 0.1 were used for HGT network analysis.

### Sequence Identity Analysis

All-vs-all ANI and alignment fraction for de-replicated plasmid sequences were computed with Vclust.

---

## Data Availability

> **[PLACEHOLDER]** Genome assemblies and plasmid sequences will be deposited at [repository] under accession numbers [XXX]. Raw sequencing reads are available at [repository] under BioProject [XXX].

## Author Contributions

> **[PLACEHOLDER]** To be completed using the CRediT taxonomy.

## Funding

> **[PLACEHOLDER]**

## Conflict of Interest

> **[PLACEHOLDER]**

## Acknowledgments

> **[PLACEHOLDER]**

---

## References

> References marked **[NEW REF — verify]** in the text must be identified, verified, and added here. Two original placeholder citations in the notes (`[cite here]()` in the BGC section; `[cite]()` in the plasmid size section) must also be resolved by the author.

- [ref 1](https://doi.org/10.1186/1471-2164-12-235)
- [ref2](https://doi.org/10.1371/journal.pcbi.1004478)
- [Wong, Finan & Golding (2002)](https://doi.org/10.1007/s10142-002-0068-0)
- [Hawkey et al. (2022)](https://doi.org/10.1099/mgen.0.000807)
- [Carattoli et. al (2005)](https://doi.org/10.1016/j.mimet.2005.03.018)
- [Garcillán-Barcia et. al (2009)](https://doi.org/10.1111/j.1574-6976.2009.00168.x)
- [Redondo-Salvo et. al (2020)](https://doi.org/10.1038/s41467-020-17278-2)
- [Shapiro et. al](https://doi.org/10.1038/s41396-023-01373-5)
- [Arredondo-Alonso et. al](https://doi.org/10.1038/s41467-025-57940-1)
- [Lipworth et. al](https://doi.org/10.1038/s41467-024-45761-7)
- [Matlock et. al](https://doi.org/10.1038/s41396-021-00926-w)
- [Fiamenghi et. al](https://doi.org/10.1038/s41467-025-65102-6)
- [Acman et al. (2020)](https://doi.org/10.1038/s41467-020-16282-w)
- [Gorbitz et. al (2025)](https://doi.org/10.1128/mbio.02497-25)
- [Pfeifer et. al (2021)](https://doi.org/10.1093/nar/gkab064)
- [Pfeir et al. (2024)](https://doi.org/10.1038/s41467-024-45757-3)
- [Cavassim et. al (2020)](https://doi.org/10.1099/mgen.0.000351)
- [del Solar et. al (1998)](https://www.ncbi.nlm.nih.gov/pubmed/9618448)
- [Cevallos et al. (2008)](https://doi.org/10.1016/j.plasmid.2013.08.001)
- [Orlek A. et al. (2023)](https://doi.org/10.1016/j.plasmid.2023.102684)
- [diCenzo & Finan (2015)](https://doi.org/10.1007/s00438-015-0998-6)
- [Patel et al. (2014)](https://doi.org/10.1099/mic.0.079137-0)
- [Mercado-Blanco & Toro (1996)](https://www.apsnet.org/publications/mpmi/BackIssues/Documents/1996Articles/Microbe09-535.pdf)
- [Luchetti et al. (2023)](https://doi.org/10.1371/journal.pone.0318411)
- [Effe et al. (2025)](https://doi.org/10.1038/s41467-025-62473-8)
- [Bethke et al. (2023)](https://doi.org/10.1093/molbev/msae206)
- [Akarsu et al. (2019)](https://doi.org/10.1371/journal.pcbi.1006946)
- [Shaw et al. (2023)](https://doi.org/10.1093/nar/gkad452)
- [Yamamoto et al. (2009)](https://doi.org/10.1128/jb.00124-09)
- [Ingmer & Cohen (1993)](https://doi.org/10.1128/jb.175.24.7834-7841.1993)
- [Hall et al. (2022)](https://doi.org/10.1098/rstb.2020.0472)
- [Qu et al. (2019)](https://doi.org/10.2147/IDR.S189168)
- [Wang et al. (2021)](https://doi.org/10.3389/fmicb.2021.754931)
- [Belogurov et al. (2000)](https://doi.org/10.1006/jmbi.1999.3493)
- [González-Montes et al. (2020)](https://doi.org/10.1371/journal.pgen.1008750)
- [Ferri et al. (2010)](https://doi.org/10.1016/j.plasmid.2010.01.001)
- [Dohlemann et al. (2016)](https://doi.org/10.1016/j.jbiotec.2016.06.033)
- [diCenzo et al. (2022)](https://doi.org/10.1128/mSystems.01092-21)
- [Passeri et al. (2025)](https://doi.org/10.1093/gbe/evae245)
- [Brom et al. (2014)](https://doi.org/10.1007/978-1-4614-9203-0_3)
- [Castellani et al. (2026)](https://doi.org/10.1128/spectrum.03242-25)
- [Kudryavtseva et al. (2023)](https://doi.org/10.3389/fmicb.2023.1133144)
- [Capela et al. (2001)](https://doi.org/10.1073/pnas.161294398)
- [Wangthaisong et al. (2024)](https://doi.org/10.3390/biology13060415)
- [Ni et al. (2021)](https://doi.org/10.1073/pnas.2011577118)
- [Sabnis et. al](https://doi.org/10.1016/j.celrep.2025.116456)
- [Selbitschka et al. (2006)](https://doi.org/10.1007/s00248-006-9056-6)
- [Schuleter et. al (2007)](https://doi.org/10.1111/j.1574-6968.2007.00731.x)
- [Douarre et. al (2020)](https://doi.org/10.3389/fmicb.2020.00483)
- [Orlek et. al (2017)](https://doi.org/10.3389/fmicb.2017.00182)
- [Szuplewska et al. (2014)](https://doi.org/10.1080/2159256X.2014.998537)
- [Liu et al. (2025)](https://doi.org/10.1093/jac/dkaf309)
- [Ipoutcha et al. (2026)](https://doi.org/10.64898/2026.01.09.696371)
- [Penadez et. al (2026)](https://doi.org/10.64898/2026.01.09.696371)
- [de la cruz et al. (2010)](https://doi.org/10.1128/mmbr.00020-10)
- [Sharma et al. (2019)](https://doi.org/10.1016/j.ijmm.2019.151354)
- [Liag et al. (2022)](https://doi.org/10.3389/fimmu.2022.899890)
- [Tran et al. (2016)](https://doi.org/10.1371/journal.ppat.1005686)
- [Park et al. (2019)](https://doi.org/10.1128/mbio.02805-18)
- [Hawes et al. (2011)](https://doi.org/10.1016/j.plantsci.2011.02.007)
- [Bustamante et al. (2023)](https://doi.org/10.1371/journal.pgen.1010776)
- [Maillet et al. (2019)](https://doi.org/10.1111/tpj.14625)
- [Schalk et al. (2025)](https://doi.org/10.1038/s41579-024-01090-6)
- [Si et al. (2025)](https://doi.org/10.1093/ismejo/wraf280)
- [Dimitriu et al. (2019)](https://doi.org/10.1098/rspb.2019.1110)
- [He et al. (2026)](https://doi.org/10.1128/jb.00536-25)
- [Low et. al (2022)](https://doi.org/10.1038/s41564-022-01146-4)
- [lacovelli et al. (2021)](https://doi.org/10.1093/jimb/kuab045)
- [Fira et al. (2018)](https://doi.org/10.1016/j.jbiotec.2018.07.044)
- [Ranjan et al. (2023)](https://doi.org/10.3390/fermentation9070597)

---

*Draft generated: 2026-06-03. Sections marked DISCREPANCY require author review. References marked [NEW REF — verify] require DOI verification. Two placeholder citations in BGC and plasmid-size sections must be resolved by the author.*
