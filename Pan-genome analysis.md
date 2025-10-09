***



# Pan-Genome Analysis
****


> [!NOTE]
> 
> Everything related with pan-genome will be stored in the following folder: [pan-genome](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/)


# Rm1021 vs MAG215
***
With the observed conservation variation between MAG215 and Sankari's RM1021 during genome synteny analysis, we decided to run a pan-genome analysis with ***Roary***.

A pan-genome analysis can give us genes comparison between the reference and the MAG215 strain. We found the core genome for these two strains is made of **74.2%** leaving a **25.8%** of variable genes (Shell genes).

| Pan-genome                            | \# genes |
|---------------------------------------|----------|
| Core genes (99% \<= strains \<= 100%) | 5447     |
| Shell genes (15% \<= strains \< 95%)  | 1888     |
| Total genes (0% \<= strains \<= 100%) | 7335     |

**After discussion with Siva, we decided to try lower thresholds of protein identity** in order to try to reduce the number of unique genes assigned to each strain (the 1888 genes above). However after trying 90, 80 and 50% few changes in number of unique genes were observed.


#### Important files

[gene_presence_absence_all_pct.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/gene_presence_absence_all_pct.xlsx)  contains the clustering for both strains MAG215 and Rm1021 using 95, 90, 80 and 50% identity percentages. 


***Clustering at 50%***

[gene_presence_absence.csv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/roary_result_50_pct/gene_presence_absence.csv) is the original file which contains a table with all the genes clustered for both genomes.

***Clustering at 80%***

[gene_presence_absence.csv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/roary_result_80_pct/gene_presence_absence.csv) is the original file which contains a table with all the genes clustered for both genomes.

***Clustering at 90%***

[gene_presence_absence.csv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/roary_result_90_pct/gene_presence_absence.csv) is the original file which contains a table with all the genes clustered for both genomes.

***Clustering at 95%***

[gene_presence_absence_all_genome.csv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/roary_result_95_pct/gene_presence_absence_all_genome.csv) is the original file which contains a table with all the genes clustered for both genomes.

[gene_presence_absence.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/roary_result_95_pct/gene_presence_absence.xlsx) is a modified form which contains two extra spreadsheets for accessory genes for MAG215 and RM1021 with an additional column (contig loc) indicating where is the gene coming from.

[pan_genome_reference.fa](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/roary_result/pan_genome_reference.fa) contains a single representative nucleotide sequence from each of the clusters in the pan genome (core and accessory). The name of each sequence is the source sequence ID followed by the cluster it came from.


**Some counts for the accessory genes:**

| Strain | Accessory genes | Hypothetical proteins | Hits with no ref |
|--------|-----------------|-----------------------|------------------|
| RM1021 | 849             | 141                   | 4                |
| MAG215 | 1039            | 255                   | 7                |
| Total  | 1888            | 396                   | 11               |



# All vs All in-house strains
****

Using the strains of *S .meliloti* assembled previously (see this [table](https://webfs/n/projects/jp2992/stowers-notes/Project-report-cbio.mm2883.102.html#descriptive-stats)), we performed a pan-genome analysis using ***Roary***. Results are showed below for 50% and 80%.

**50%**

[pangenome_matrix.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/between_in_house_strains//roary_result_50_pct_1751912799/pangenome_matrix.png) shows a matrix of presence/absence of accessory genome next to the dendrogram grouping samples by accessory genome.

[set_difference_unique_set_one_statistics.csv](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/between_in_house_strains/roary_result_50_pct_1751912799/set_difference_unique_set_one_statistics.csv) presents genes unique to MAG215 (H01).

| Gene Category   | Strain Frequency Range | Number of Genes |
| --------------- | ---------------------- | --------------- |
| Core genes      | 99% ≤ strains ≤ 100%   | 4933            |
| Soft core genes | 95% ≤ strains < 99%    | 0               |
| Shell genes     | 15% ≤ strains < 95%    | 2348            |
| Cloud genes     | 0% ≤ strains < 15%     | 1981            |
| Total genes     | 0% ≤ strains ≤ 100%    | 9262            |


**80%** 

[pangenome_matrix.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/between_in_house_strains/roary_result_80_pct_1751912805/pangenome_matrix.png) shows a matrix of presence/absence of accessory genome next to the dendrogram grouping samples by accessory genome.

[set_difference_unique_set_one_statistics.csv](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/between_in_house_strains/roary_result_80_pct_1751912805/set_difference_unique_set_one_statistics.csv) presents genes unique to MAG215 (H01).

| Gene Category   | Strain Frequency Range | Number of Genes |
| --------------- | ---------------------- | --------------- |
| Core genes      | 99% ≤ strains ≤ 100%   | 4920            |
| Soft core genes | 95% ≤ strains < 99%    | 0               |
| Shell genes     | 15% ≤ strains < 95%    | 2324            |
| Cloud genes     | 0% ≤ strains < 15%     | 2162            |
| Total genes     | 0% ≤ strains ≤ 100%    | 9406            |


Once again, like during QUAST assessment, in terms of accessory genome we see F1 as the genome that shares more features with MAG215 (H01).

# Public MAG strains
***
We observed no significant reduction between MAG215 and Rm1021 (the max. reduction was 200 genes between 95% and 50%), one reason for this may be the divergence between strains. Therefore, **we will try to use MAG strains from other authors for which Madi had information about which ones had susceptibility** in a attempt to make a reconstruction of MAG215 genome using susceptible strains to find unique zones in MAG215 involved with resistance. 

## MAG assemblies metadata

Bioinformatician Daniel provided me with the MAG genomes downloaded for a previous work. According to Daniel's report, Information about these strains were  retrieved from [Batstone et. al 2022](https://doi.org/10.1098/rspb.2022.0477)

Below, important documents hosting genomes and metadata:

* [Accession per MAG strain.tsv](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.101/data/MAG_key.tsv): Accession code for the MAG strains genomes included in the folder below (87).
* [Smeliloti genomes](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.101/data/Genbank_09.24): Folder with several *S. meliloti* genomes retrieved form the NCBI (471).
* [MAG strains metadata.tsv](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.101/data/MAG_metadata.tsv) Contains information about MAG strains genome assemblies. 
* [Daniel's report](https://webfs/n/core/Bioinformatics/analysis/Sankari/mm2883/cbio.mm2883.101/code/report.html): Report that Daniel produced for a previous work with Siva. The are some information about the MAG strains. 
* [MAG_assembly_metadata.tsv](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/MAG_assembly_metadata.tsv) Contains extra metadata about the MAG assemblies.


> [!NOTE]
> During processing of  [MAG_assembly_metadata.tsv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/MAG_assembly_metadata.tsv) we realized there were some genomes with completeness bellow 99, in order to establish a good core-genome we need assemblies as complete as possible. During this [notebook](https://webfs//n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/mag_metadata.ipynb) I filtered to keep only genomes with completeness > 99% according to CheckM and saved in [keys_best_asm.tsv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/keys_best_asm.tsv) . **It was retained 77 out of 89 MAG genomes**. 
> The retained genomes were stored at [best_asm_mag](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/best_asm_mag/)



### Best MAG assemblies stats

Below, Histograms showing distribution of completeness (percentage), number of contigs assembled (count), N50 and L50 metric:

* [hist_completeness.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/best_asm_mag/hist_completeness.png)

* [hist_num_contigs.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/best_asm_mag/hist_num_contigs.png)

* [hist_contigN50.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/best_asm_mag/hist_contigN50.png)

* [hist_contigL50.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/best_asm_mag/hist_contigL50.png)


## Susceptible MAG strains

Madi has identified the following susceptible MAG strains:

|     | 1      | 2      | 3      | 4      | 5      | 6      | 7      | 8      |
| --- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 1   | MAG5   | MAG10  | MAG16  | MAG21  | MAG24  | MAG27  | MAG73  | MAG88  |
| 2   | MAG97  | MAG121 | MAG123 | MAG41  | MAG42  | MAG48  | MAG145 | MAG157 |
| 3   | MAG169 | MAG182 | MAG183 | MAG191 | MAG199 | MAG200 | MAG201 | MAG220 |
| 4   | MAG221 | MAG225 | MAG230 | MAG242 | MAG245 | MAG258 | MAG259 | MAG278 |
| 5   | MAG282 | MAG286 | MAG313 | MAG320 | MAG322 | MAG325 | MAG342 | MAG358 |
| 6   | MAG373 | MAG384 | MAG386 | MAG406 | MAG417 | MAG420 | MAG513 | MAG514 |
| 7   | MAG523 | MAG530 | MAG533 | MAG539 | MAG540 |        |        |        |

Since we have 86 susceptible and previously we mentioned earlier that we filtered the dataset of MAG genomes to 77. At the end, **we were abled to retrieved 52 MAG susceptible genomes with good quality metrics**. Below some histograms showing the distribution of different quality metrics across these genomes.

[descrip_stats_histo.png](https://webfs/n/projects/jp2992/MOLNG4331/genomes/MAG_genomes/susceptible_mag_genomes/descrip_stats_histo.png)


## MAG215 vs Susceptible MAG pan-genome

The idea is to check for gene unique to MAG215 that might confer resistance to the peptide. To do this I used PPanGGoLin, a tool to create and manipulate prokaryotic pan-genomes. 

The H01 unique genes were extracted with a custom python script [parse_ppanggolin_output.ipynb](https://webfs/n/projects/jp2992/MOLNG4331/code/parse_ppanggolin_output.ipynb)

**To cluster protein families I set 80% coverage and 80% identity.**

[H01_unique_genes_extended.tsv](https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/susceptible_MAG_vs_mag215/ppanggolin_results_80pct/H01_unique_genes_extended.tsv) contains the genes found only in H01 including other information provided by tool, such as RGP and genes neighboring.

###  Genome similarity between MAG215 and MAG strains

Let's check similarity between MAG215 and the others 88 MAG genomes using k-mer analysis with ***SourMash***. The following analysis basically gives us **insights** of how much of *X* genome in shared with *Y* genome. In this case, we are sampling a k-mer of 31 every 100 k-mers (scaled=100).

| Similarity | Match                       |
| ---------- | --------------------------- |
| 100.0%     | H01_asm.fasta               |
| 99.7%      | GCA_033715675.1 strain=215  |
| 72.7%      | GCA_033716695.1 strain=386  |
| 72.4%      | GCA_033714725.1 strain=749C |
| 72.3%      | GCA_033714075.1 strain=342  |
| 71.6%      | GCA_033713535.1 strain=146  |
| 71.3%      | GCA_033716305.1 strain=748A |
| 71.3%      | GCA_033714695.1 strain=733A |
| 71.2%      | GCA_033712675.1 strain=24   |
| 71.2%      | GCA_033715705.1 strain=243A |

## pMAG215 containment in other MAG strains

Using ***SourMash***, we looked for the presence of the extra plasmid found in MAG215 in the other MAG strains. We see the maximum containment was from MAG97. 

| Similarity | Match                       |
| ---------- | --------------------------- |
| 100.0%     | H01_asm.fasta               |
| 98.6%      | GCA_033715675.1 strain=215  |
| 34.9%      | GCA_033716795.1 strain=97   |
| 33.8%      | GCA_033714725.1 strain=749C |
| 32.7%      | GCA_033712485.1 strain=18   |
| 30.0%      | GCA_033716245.1 strain=743  |
| 20.0%      | GCA_033714785.1 strain=180  |
| 19.4%      | GCA_033712715.1 strain=50   |
| 19.3%      | GCA_033713635.1 strain=228A |
| 19.1%      | GCA_033712675.1 strain=24   |

In this [QUAST](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/quast/icarus_viewers/alignment_viewer.html) comparison it was aligned strain **MAG386** (previous table), **B02** (Sankari lab's rm1021) and **MAG97**. It allows us to see the amount of plasmid found in MAG97 and the genome coverage for its closest MAG strain and the classic Rm1021.


