
# Sinorhizobium meliloti assembly
***
**Authors:** Andrew Price and Juan Jose Picon Cossio

# Objective 

Assemble 9 Smeliloti strain genomes (it was supposed to be 10, but the demultiplexing for one of the samples failed) for the Sankari lab.

**To start,** they're interested in their lab-version of the RM1021 (B02) reference strain and the MAG215 (H01) strain that Madi is working with.


# Data description

- Reads location: [MOLNG4331](https://webfs/n/analysis/Sankari/mm2883/MOLNG-4331/EA156900/LongPlex/longplex_output/MOLNG4331/merged_fastq/)
- [multiqc_report.html](https://webfs/n/projects/jp2992/MOLNG4331/merged_fastq/QC/multiqc_report.html) Quality report.
- Reads are from different *S. meliloti* strains, except one which was a pseudomonas.
- **Reads H01 and B02 corresponding to strains MAG215 and RM1021 (reference), respectively.**

| Library Name | Adapter Type | Index Label |     |
| ------------ | ------------ | ----------- | --- |
| Rm1021       | PacBio       | B02         | 1   |
| KH46         | PacBio       | A02         | 2   |
| MAG215       | PacBio       | H01         | 3   |
| MAG177       | PacBio       | G01         | 4   |
| MAG176-B     | PacBio       | F01         | 5   |
| MAG154*      | PacBio       | E01         | 6   |
| MAG121       | PacBio       | D01         | 7   |
| MAG62        | PacBio       | C01         | 8   |
| MAG31**      | PacBio       | B01         | 9   |
| MAG18        | PacBio       | A01         | 10  |
|              |              |             |     |

\* Pseudomonas contamination.
** No sequencing available. Library prep-related problems.

[resistant_strains.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/resistant_strains.xlsx) contains the resistant and susceptible strains. Pink and Green cells will be ignored.
[susceptible_mag_codes.txt](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/susceptible_mag_codes.txt) 

|     | 1      | 2      | 3      | 4      | 5      | 6      | 7      | 8      |
| --- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 1   | MAG5   | MAG10  | MAG16  | MAG21  | MAG24  | MAG27  | MAG73  | MAG88  |
| 2   | MAG97  | MAG121 | MAG123 | MAG41  | MAG42  | MAG48  | MAG145 | MAG157 |
| 3   | MAG169 | MAG182 | MAG183 | MAG191 | MAG199 | MAG200 | MAG201 | MAG220 |
| 4   | MAG221 | MAG225 | MAG230 | MAG242 | MAG245 | MAG258 | MAG259 | MAG278 |
| 5   | MAG282 | MAG286 | MAG313 | MAG320 | MAG322 | MAG325 | MAG342 | MAG358 |
| 6   | MAG373 | MAG384 | MAG386 | MAG406 | MAG417 | MAG420 | MAG513 | MAG514 |
| 7   | MAG523 | MAG530 | MAG533 | MAG539 | MAG540 |        |        |        |

# Assembly assessment
***
Everything related with the assembly of *S. meliloti*

## Visualization 
This first analysis was done using the two strains Siva and Madi were interested in the beginning. It helped us visualize differences between ***Hifiasm*** and ***Flye*** for this bacteria.

- **1a** and **1b** are Hifiasm for H01 and B02, respectively.
- **2a** and **2b** are Flye for H01 and B02, respectively.

As expected, genomes for both strain are at chromosome level. We can see a concordance between both tools during genome assembly of B02 (RM1021) with both of them presenting 3 big contigs. Hifiasm and Flye presented comparable contig sizes for both strains. However, **MAG215 (H01) presents and extra short contig circularized in Flye** (2a, short green line), but not in Hifiasm (1a, short purple line with blue edges) suggesting a possible extra plasmid.

The extra contig size was significantly different between Flye and Hifiasm, with Hifiasm having 40kb more than Flye's. See [Putative plasmid analysis (pMAG215)](https://webfs/n/projects/jp2992/stowers-notes/Project-report-cbio.mm2883.102.html#putative-plasmid-analysis-pmag215) for information about this extra contig description. 


| <img  src="https://webfs/n/projects/jp2992/stowers-notes/photos/assembly_bandage.png" class="wikilink" alt="assembly_bandage.png" /> |
| ------------------------------------------------------------------------------------------------------------------------------------ |
| **Figure 1.** Genome assembly for RM1021 (bottom row) and MAG215 (top row) using Hifiasm (left column) and Flye (right column)       |

## Descriptive stats
The table below presents descriptive stats of the nine *S. meliloti* assembled genomes. **The highlighted in bold corresponds to an impostor which is a *pseudomona*.**

| file                   | type    | # seqs | sum_len       | min_len     | avg_len         | max_len       |
| ---------------------- | ------- | ------ | ------------- | ----------- | --------------- | ------------- |
| A01_asm_flye.fasta     | DNA     | 5      | 6,919,858     | 139,932     | 1,383,971.6     | 3,593,188     |
| A02_asm_hifiasm.fasta  | DNA     | 3      | 7,034,387     | 1,597,380   | 2,344,795.7     | 3,753,122     |
| B02_asm_flye.fasta     | DNA     | 3      | 6,696,400     | 1,355,887   | 2,232,133.3     | 3,657,162     |
| C01_asm_flye.fasta     | DNA     | 3      | 6,926,656     | 1,494,128   | 2,308,885.3     | 3,735,505     |
| D01_asm_flye.fasta     | DNA     | 3      | 6,746,538     | 1,305,092   | 2,248,846       | 3,835,146     |
| **E01_asm_flye.fasta** | **DNA** | **2**  | **5,882,655** | **121,616** | **2,941,327.5** | **5,761,039** |
| F01_asm_flye.fasta     | DNA     | 3      | 6,744,852     | 1,415,219   | 2,248,284       | 3,710,337     |
| G01_asm_flye.fasta     | DNA     | 4      | 6,922,790     | 166,347     | 1,730,697.5     | 3,544,365     |
| H01_asm_flye.fasta     | DNA     | 4      | 6,864,704     | 192,654     | 1,716,176       | 3,654,821     |
|                        |         |        |               |             |                 |               |
33

> [!NOTE]
> 
> Given the inconsistency observed during [plasmid typing](https://webfs/n/projects/jp2992/stowers-notes/Project-report-cbio.mm2883.102.html#plasmid-typing) for A02's putative plasmid and the assembly graph file produced by Flye ([A02_asm_flye.png](https://webfs/n/projects/jp2992/MOLNG4331/flye/A02/A02_asm_flye.png)), assembly was re-done using Hifiasm and confirmed our suspicious of being an assembly error.

A01 was also fishy as, apparently, it has 2 accessory plasmid, re-assembly was done with Hifiasm and showed a same result. The assembly [A01_hifiasm.gfa](https://webfs/n/projects/jp2992/MOLNG4331/hifiasm/A01/A01.bp.p_ctg.gfa) can be visualized in Bandage.  

## Coverage

Text files (.txt) in the following folder contains histogram coverage and depth for each contig for every *S. meliloti* assembly. It also includes mean base quality and mapping quality: [Coverage](https://webfs/n/projects/jp2992/MOLNG4331/genomes/coverage/)

**In summary:**

* The range of sample coverage is 334x−761x. 

* The median coverage is 494x.

## Completeness

### QUAST
After assembling, QUAST was used to compare the strains to MAG215. We can see that the the classic reference Rm1021 (B02) is not the most similar to MAG215.

[QUAST_Results](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/quast/report.html)

### CheckM
 ***CheckM*** evaluates the completeness of the nine *S. meliloti* strains according to presence/absence of marker genes and the expected co-localization of these genes.

| Bin Id           | Marker lineage               | # genomes | # markers | # marker sets | 0   | 1    | 2   | 3   | Completeness | Contamination |
| ---------------- | ---------------------------- | --------- | --------- | ------------- | --- | ---- | --- | --- | ------------ | ------------- |
| A01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1019 | 3   | 0   | 99.59        | 0.78          |
| A02_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1021 | 1   | 0   | 99.59        | 0.31          |
| B02_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 4   | 1020 | 1   | 0   | 99.28        | 0.31          |
| C01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1020 | 2   | 0   | 99.59        | 0.47          |
| D01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1022 | 0   | 0   | 99.59        | 0.00          |
| **E01_asm_flye** | **g__Pseudomonas (UID4526)** | 38        | 1397      | 371           | 5   | 1364 | 27  | 1   | 99.61        | 2.58          |
| F01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1022 | 0   | 0   | 99.59        | 0.00          |
| G01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1021 | 1   | 0   | 99.59        | 0.31          |
| H01_asm_flye     | g__Ensifer(UID3566)          | 27        | 1025      | 322           | 3   | 1019 | 3   | 0   | 99.59        | 0.49          |


### Liftoff

To get us started on finding the genes in the two different assemblies, I ran liftoff to trasnfer the gene annotations from the reference strain to our assemblies. For reference, the reference gene model contains 6298 genes.

The mag215 strain was able to have 5698 of those genes mapped over, missing out on 600 on them, either due to the gene completely being missing in this strain or having evolved past the point of LiftOff being able to map them.

Here's the mag215 gtf after liftoff:  
[mag215_liftoff_gtf](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.102/data/mag215/liftoff.mag215.gtf)

Here's a list of the 600 genes unable to be mapped:  
[mag215_liftoff_missing](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.102/data/mag215/liftoff.mag215.unmapped.gtf)

On the other hand, every single gene was able to be mapped to the rm1021 strain, which a great sign that our assembly is good:
[rm1021_liftoff_gtf](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.102/data/rm1021/liftoff.rm1021.gtf)


# Genome annotation

Genome annotation of all strains was performed with ***PGAP*** the pipeline developed by the NCBI. 

All annotation are inside each assembly's folder under a folder named *pgap_annotation*. 
[assemblies](https://webfs/n/projects/jp2992/MOLNG4331/flye) 

> [!TODO]
> I want to change this folder organization as I will implement more annotation tools 

# Genome synteny
***

## All vs MAG215

Genome alignment was performed between all the strains assembled against MAG215. The alignment includes the B02 (Rm1021) which might help to rule out genomic regions. 

In this file we can observed a dot plot of the whole genome alignment for all the strains against MAG215 [all_vs_mag215_asm20.paf.pdf](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/minimap2/all_vs_mag215_asm20.paf.pdf)

For a more interactive view in this [igv session](https://webfs/n/projects/jp2992/MOLNG4331/flye/genomes/genome_comparison/minimap2/igv_session.xml) you can observed the alignment including the annotation for MAG215. 

Below some descriptive stats of the alignment of a min alignment length of 5000 and mean quality of 30. We see high chromosome and super-plasmids coverage, but not for the accessory plasmid.

| name         | size    | numreads | covbases | coverage | meandepth | meanmapq |
| ------------ | ------- | -------- | -------- | -------- | --------- | -------- |
| contig_1_H01 | 1689003 | 118      | 1670705  | 98.9166  | 6.54925   | 60       |
| contig_2_H01 | 3654821 | 194      | 3551763  | 97.1802  | 6.65477   | 59.8     |
| contig_3_H01 | 1328226 | 214      | 1310964  | 98.7004  | 5.16338   | 59.8     |
| contig_4_H01 | 192654  | 39       | 126563   | 65.6945  | 0.876483  | 59.9     |

**I will try minigraph-cactus as an alternative to progressiveMauve since I do not like the output of it**






## MAG215 vs Rm1021
Genome synteny analysis with ***progressiveMauve*** showed significant levels of rearrangements in MAG215 compared to RM1021, as well as different levels of conservation per synteny block and unique zones to MAG215 and RM1021.

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/synteny_backbone.jpg" class="wikilink"
alt="synteny_backbone.jpg" />
<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/synteny.jpg" class="wikilink" alt="synteny.jpg" /> 

**Figure 2.** Genome to genome alignment. For both pictures, first and second row are NCBI's RM1021 and Sankari lab's RM1021, respectively. Third row is MAG215 and also the reference for alignment orientation. **Top picture** showing backbone analysis; pink, conserved regions in all strains; green, conserved regions only between Rm1021; no color, unaligned regions. **Bottom picture** is showing synteny blocks; no color are unaligned regions; inside each synteny block, bars represents similarity profile. Blocks over the line were aligned in forward and below in reverse complement.


# Pan-genome analysis
Everything related with pan-genome is in  [Pan-genome analysis](https://webfs/n/projects/jp2992/stowers-notes/Pan-genome%20analysis.html)

# Plasmids information
****

Everything related with accessory Plasmid assessment.

## Plasmid typing
****

During [Putative plasmid analysis](https://webfs/n/projects/jp2992/stowers-notes/Project-report-cbio.mm2883.102.html#putative-plasmid-analysis-pmag215) we learned that *S. meliloti* can hold accessory plasmids. 

More plasmids were found in the rest of the strains. Therefore, we will type them to identify its existence. To do so we will take into account the **coverage** and the **plasmid-related proteins**.

### Coverage

Table below presents descriptive stats from Flye for all putative accessory plasmids for all strains. We can see that they have a mean coverage high consistent with the rest of the genome.  

With Flye's report we noticed that A02's plasmid had apparent unsolved path with the main chromosome which hindered its circularization, and the assembler decided to split the sequence from the chromosome. Plasmid-related proteins will help us solve this.

| sample | seq_name | length | cov. | circ. | graph path |
| ------ | -------- | ------ | ---- | ----- | ---------- |
| A01    | contig_3 | 256854 | 471  | Y     |            |
| A01    | contig_1 | 139932 | 434  | Y     |            |
| A02*   | contig_3 | 288326 | 536  | N     | 1,3        |
| G01    | contig_3 | 166347 | 678  | Y     |            |
| H01    | contig_4 | 192654 | 772  | Y     |            |
\* Determined as assembly error. See *assembly assessment* section

### Plasmid-related features 

1. Relaxases proteins.
2. Mating Pair Formation system (MPF).
3. OriV.
4. Replication Initiation Protein (RIP).

***MOB Suites*** was used for identify **1 & 2**.

| sample_id        | size   | gc   | rep_type(s)     | rep_type_accession(s)   | relaxase_type(s) | relaxase_type_accession(s) | mpf_type | mpf_type_accession(s)                                                                           | predicted_mobility | mash_nearest_neighbor | mash_neighbor_distance | mash_neighbor_identification | primary_cluster_id | secondary_cluster_id | predicted_host_range_overall_rank | predicted_host_range_overall_name |
| ---------------- | ------ | ---- | --------------- | ----------------------- | ---------------- | -------------------------- | -------- | ----------------------------------------------------------------------------------------------- | ------------------ | --------------------- | ---------------------- | ---------------------------- | ------------------ | -------------------- | --------------------------------- | --------------------------------- |
| **contig_3_A02** | 288326 | 0.62 | -               | -                       | -                | -                          | -        | -                                                                                               | non-mobilizable    | CP021807              | 0.219531               | Sinorhizobium meliloti       | AA612              | AI850                | -                                 | -                                 |
| contig_3_A01     | 256854 | 0.58 | rep_cluster_471 | 001821__NC_018682_00001 | MOBP             | CP026529_00118             | MPF_T    | NC_009621_01097,NC_017324_00907,NC_017324_00906,NC_017324_00904,NC_017324_00902,NC_009621_01115 | conjugative        | NC_019847             | 0.080322               | Sinorhizobium meliloti GR4   | AA614              | AI853                | family                            | Rhizobiaceae                      |
| contig_4_H01     | 192654 | 0.58 | rep_cluster_471 | 001821__NC_018682_00001 | MOBP             | CP026529_00118             | -        | -                                                                                               | mobilizable        | CP021832              | 0.0716227              | Sinorhizobium meliloti       | AA618              | AI857                | family                            | Rhizobiaceae                      |
| contig_3_G01     | 166347 | 0.59 | rep_cluster_546 | 001918__NC_013545_00001 | MOBP             | CP026529_00118             | MPF_T    | NC_016814_00035,NC_019313_00276,NC_017327_00230,NC_017327_00231,NC_009622_00075                 | conjugative        | CP003934              | 0.00793                | Sinorhizobium meliloti GR4   | AA610              | AI848                | genus                             | Sinorhizobium                     |
| contig_1_A01     | 139932 | 0.58 | -               | -                       | MOBP             | CP026529_00118             | MPF_T    | NC_009622_00075,NC_017327_00231,NC_017327_00230,NC_019313_00276,NC_016814_00035                 | conjugative        | CP003934              | 0.109331               | Sinorhizobium meliloti GR4   | AA610              | AI848                | genus                             | Sinorhizobium                     |

**We can observe that A02's plasmid was not predicted with a relaxase-type protein, nor a MPF, additionally presents a GC content more similar to the chromosome than to the other plasmids.**

Through the annotation with ***PGAP*** we can identify **4**. Below, we see that using the GFF, **we were abled to retrieved a RepABC for all putative plasmids except for A02**. This supports the idea of being an assembly artifact.

| File          | Feature | Start  | End    | Strand | Gene |
| ------------- | ------- | ------ | ------ | ------ | ---- |
| A01_annot.gff | CDS     | 69939  | 71153  | -      | repC |
| A01_annot.gff | CDS     | 71308  | 72291  | -      | repB |
| A01_annot.gff | CDS     | 72288  | 73484  | -      | repA |
| A01_annot.gff | CDS     | 77376  | 78653  | -      | repC |
| A01_annot.gff | CDS     | 40003  | 41217  | -      | repC |
| A01_annot.gff | CDS     | 41418  | 42437  | -      | repB |
| A01_annot.gff | CDS     | 42434  | 43657  | -      | repA |
| A01_annot.gff | CDS     | 159514 | 160791 | +      | repA |
| G01_annot.gff | CDS     | 152673 | 153950 | +      | repC |
| G01_annot.gff | CDS     | 157959 | 159161 | +      | repA |
| G01_annot.gff | CDS     | 159158 | 160192 | +      | repB |
| G01_annot.gff | CDS     | 160366 | 161580 | +      | repC |
| H01_annot.gff | CDS     | 176279 | 177493 | -      | repC |
| H01_annot.gff | CDS     | 177693 | 178712 | -      | repB |
| H01_annot.gff | CDS     | 178709 | 179932 | -      | repA |

 ***OriV-Finder*** was abled to report **3** thanks to the predictions of RIP proteins, this tool uses its own HMM searches, but in the previous table we can see that PGAP also predicted RIP proteins for all of the plasmids, the complete module RepABC. However, some plasmids also had matches with OriC in the database DoriC.

* **A01 contig 1:**
[RIP and OriV positions](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/A01_contig_1_OriV_prediction/Genome_Viz.html)  [OriV details](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/A01_contig_1_OriV_prediction/OriV_Viz.html)

* **A01 contig 3:**
[RIP and OriV positions](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/A01_contig_3_OriV_prediction/Genome_Viz.html)  [OriV details](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/A01_contig_3_OriV_prediction/OriV_Viz.html)

* **G01**
[RIP and OriV positions](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/G01_OriV_prediction/Genome_Viz.html)  [OriV details](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/G01_OriV_prediction/OriV_Viz.html)

* **H01**
[RIP and OriV positions](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/H01_OriV_prediction/Genome_Viz.html)  [OriV details](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/H01_OriV_prediction/OriV_Viz.html)



## Plasmid annotation 
****
You can find gene annotation for each plasmid in [plasmids_smeliloti](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/). Each plasmid has an annotation folder in the form of **\[A-Z\]\[0-9\]{2}\_pgap\_annot**, for example, annotation for genome **A01** is **A01_pgap_annot** and so on.

Summary stats of annotation for each plasmid:

| Sample           | Type       | Number   | Size total (kb) | Size mean (bp) |
| ---------------- | ---------- | -------- | --------------- | -------------- |
| A01_contig_1     | cds        | 152      | 113.40          | 746.03         |
| A01_contig_1     | gene       | 128      | 99.59           | 778.05         |
| A01_contig_1     | pseudogene | 24       | 13.81           | 575.25         |
| A01_contig_1     | region     | 1        | 139.93          | 139932.00      |
| **A01_contig_1** | **Total**  | **609**  | 593.52          | 974.58         |
| A01_contig_3     | cds        | 279      | 201.10          | 720.80         |
| A01_contig_3     | gene       | 200      | 156.38          | 781.88         |
| A01_contig_3     | pseudogene | 80       | 44.80           | 560.00         |
| A01_contig_3     | region     | 1        | 256.85          | 256854.00      |
| A01_contig_3     | trna       | 1        | 0.07            | 71.00          |
| **A01_contig_3** | **Total**  | **1120** | 1061.48         | 947.75         |
| G01              | cds        | 175      | 139.73          | 798.47         |
| G01              | gene       | 165      | 135.45          | 820.90         |
| G01              | pseudogene | 10       | 4.28            | 428.40         |
| G01              | region     | 1        | 166.35          | 166347.00      |
| **G01**          | **Total**  | **701**  | 725.27          | 1034.63        |
| H01              | cds        | 225      | 151.45          | 673.11         |
| H01              | gene       | 182      | 126.45          | 694.79         |
| H01              | pseudogene | 43       | 25.00           | 581.35         |
| H01              | region     | 1        | 192.65          | 192654.00      |
| **H01**          | **Total**  | **901**  | 798.45          | 886.19         |



## Plasmid homology 
### Between public plasmids

I will use the same [dataset with 114 sequences](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/plasmids_smeliloti_filtered.fasta), collected when we were confirming pMAG215, to find if the other 3 plasmids were reported before or are also new ones.

> [!Update]
> 
> I updated the dataset to include more sequences [ref_smeliloti_plasmids_filt.fasta](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/ref_smeliloti_plasmids_filt.fasta) 
> 
> It was not used here though.


| rname        | endpos | numreads | covbases | coverage | meandepth | meanmapq |
| ------------ | ------ | -------- | -------- | -------- | --------- | -------- |
| contig_1_A01 | 139932 | 99       | 104765   | 74.8685  | 2.259     | 48.5     |
| contig_3_A01 | 256854 | 738      | 180208   | 70.1597  | 5.84001   | 44.4     |
| contig_3_G01 | 166347 | 217      | 165616   | 99.5606  | 8.36703   | 47.9     |
| contig_4_H01 | 192654 | 260      | 109934   | 57.0629  | 2.32121   | 43.7     |

[igv_session](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/homology/public_plasmids_vs_plasmids_in_house/igv_session.xml) here we can observed the alignments. 

G01 is the most covered plasmid, with some plasmids covering up to 89% with >98% identity, although it still has some unique regions observed as long insertions, there is high probability that they are same plasmid.

The rest of the plasmids are partially covered with plasmids covering no more than 40%. Indicating these might be new plasmids like pMAG215.  



### Between in-house strains
#### All vs pMAG215
Minimap2 (asm20) was used to get insight of regions shared between the plasmids and pMAG215.

[all_vs_pmag215_asm20](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/homology/all_vs_pmag215/out.pdf) shows dot plot with coverage of the 3 in-house plasmids to pMAG215 using Minimap2-asm20 

When can observed the alignments selecting contig_4 (pMAG215) in [igv session](https://webfs/n/projects/jp2992/MOLNG4331/flye/genomes/genome_comparison/minimap2/igv_session.xml). **This is the same alignment presented in genome synteny section**.

#### All vs All plasmids

Roary was used to observe set of genes shared by the 4 plasmids, using 80% and 50% identity.

[roary folder](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/roary/) in this folder you can find results for 80% (\*\_80pct_\*) and 50% (\*\_50pct_) in each folder there is a folder called fixed_input_files/ which contains the GFF to look for genes reported in the CSV file **gene_presence_absence.csv**

**Summary:** 

**80%**

[pangenome_matrix.png](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/roary/roary_result_80_pct/pangenome_matrix.png) left a binary tree built with accessory genome. Right matrix of presence/absence of accessory genome. 

| Gene Category   | Strain Frequency Range | Number of Genes |
| --------------- | ---------------------- | --------------- |
| Core genes      | 99% ≤ strains ≤ 100%   | 5               |
| Soft core genes | 95% ≤ strains < 99%    | 0               |
| Shell genes     | 15% ≤ strains < 95%    | 512             |
| Cloud genes     | 0% ≤ strains < 15%     | 0               |
| **Total genes** | 0% ≤ strains ≤ 100%    | **517**         |


**50%**

| Gene Category   | Strain Frequency Range | Number of Genes |
| --------------- | ---------------------- | --------------- |
| Core genes      | 99% ≤ strains ≤ 100%   | 9               |
| Soft core genes | 95% ≤ strains < 99%    | 0               |
| Shell genes     | 15% ≤ strains < 95%    | 462             |
| Cloud genes     | 0% ≤ strains < 15%     | 0               |
| **Total genes** | 0% ≤ strains ≤ 100%    | **471**         |

We can see that small number of genes are shared across all 4 plasmids, probably indicating about different functions associated to each of them. However, during alignment of the 3 plasmids against pMAG215 we were abled to see differences in similarity between plasmids, for example, we can see that A01 is apparently the most similar sharing almost 50 % of the plasmid sequence.



## Plasmid copy number 

All of them were predicted to be 1 copy number by *Plassembler* (based on *Unicycler*) which uses coverage comparison against chromosome.

| code | contig       | length  | depth  | copy number |
| ---- | ------------ | ------- | ------ | ----------- |
| A01  | chromosome   | 1264915 | 558.67 | 1           |
| A01  | chromosome_2 | 3593188 | 384.48 | 0.69        |
| A01  | chromosome_3 | 1664969 | 468.34 | 0.84        |
| A01  | 1            | 256854  | 467.75 | 0.84        |
| A01  | 2            | 139932  | 432.28 | 0.77        |
| G01  | chromosome   | 1682661 | 501.82 | 1           |
| G01  | chromosome_2 | 3544365 | 526.2  | 1.05        |
| G01  | chromosome_3 | 1529417 | 579.84 | 1.16        |
| G01  | 1            | 166347  | 671.13 | 1.34        |
| H01  | chromosome   | 1689003 | 547.89 | 1           |
| H01  | chromosome_2 | 3654821 | 558.88 | 1.02        |
| H01  | chromosome_3 | 1328226 | 614.05 | 1.12        |
| H01  | 1            | 192654  | 753.57 | 1.38        |


<details>
<summary > Show command </summary>

```
target=("A01" "G01" "H01")

task_id=$SLURM_ARRAY_TASK_ID

strain=${target[$task_id]}

echo "processing" $strain

reads=$(ls /n/analysis/Sankari/mm2883/MOLNG-4331/EA156900/LongPlex/longplex_output/MOLNG4331/merged_fastq/*.gz | grep $strain)

conda activate plassembler

plassembler long --force -l $reads -t $cpus --pacbio_model "pacbio-hifi" \

--flye_assembly /n/projects/jp2992/MOLNG4331/flye/$strain/assembly_info.fasta \

--flye_info /n/projects/jp2992/MOLNG4331/flye/$strain/assembly_info.txt \

-d /n/projects/jp2992/MOLNG4331/biocomp_tools/plsdb \

-o /n/projects/jp2992/MOLNG4331/plasmids_smeliloti/in_house_pls/$strain/
```

</details>

## Plasmidome 
Everything related with plasmidome is in [Plasmidome](https://webfs/n/projects/jp2992/stowers-notes/Plasmidome.html)


# Variant calling using core genome

For variant calling plasmid was removed before. The reason is that some part of the plasmids might be represented in the super plasmids or the chromosome, representing possible bias during alignment. Afterwards, ***Snippy*** was used for variant calling.

[snps.tab](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/snps_core_genome/snippy_result_no_plasmid/snps.tab) Contains variants with product and effect annotation.




# Putative plasmid analysis (pMAG215)
***

During MAG215 assembly an extra piece of DNA sequence was found. This extra DNA sequence was unexpected and had some features indicating it may be an accessory plasmid (size, coverage, circular), therefore it had to be analyzed separately. 

[Hunting a plasmid](https://webfs/n/projects/jp2992/stowers-notes/Hunting-a-plasmid.html) describes everything related to the plasmid.


# Collaborator *S. meliloti* genome assembly
***

## Data

* In total 119 *S. meliloti* strains were assembled and shared by a collaborator of Siva. 

* Genomes are stored in [collaborator_Smeliloti_hifi](https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/)


## Reads quality

[multiqc_report.htm](https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/raw_reads/QC/multiqc_report.html) Quality report of the PacBio reads.

We can noticed that compared to Siva's PacBio they counted with less number of reads and a smallest median read length. Given that Siva's sequencing has 10 times more data than the collaborator, I subsample to 20k reads to achieve similar amount of data as the collaborator. At the end, Siva's counted with a mean read length between 14522 -15000 bp per sample, whereas the collaborator presents median between 6249-7249 bp.

## Genome assembly

[descriptive_stats_collaborator_genomes.ipynb](https://webfs/n/projects/jp2992/MOLNG4331/code/descriptive_stats_collaborator_genomes.ipynb) custom script to parse and plot.

### Collaborator assemblies

Check [[Penn State Strains (Liana)]] 