
Plasmid reconstruction from illumina WGS assemblies represent a big challenge due to the short length and shared gene content with the chromosome and other plasmids. Even more *Sinorhizobium meliloti*  present a bigger challenge due to its mega-plasmids. Specially PsymA has been identified as a hotspot for horizontal gene transfer events. Carrying big stretches of genomic island. This brings up the question of: **How to differentiate a stretch coming from a PsymA or a an accessory plasmid?** this is a question that maybe in some cases only long reads assembly can answer. However, in isolate plasmid research it is impossible and unfeasible to sequence everything at decent coverage.

Thus, a method to predict accessory plasmids in bacteria like *S. meliloti* results useful so we select which isolates to sequence.

# Pre-processing

In of [MAG_assembly_metadata.tsv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/MAG_assembly_metadata.tsv) I realized there were some genomes with completeness < 99, in order to establish a good core-genome we need assemblies as complete as possible. During this [notebook](https://webfs//n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/mag_metadata.ipynb) I filtered to keep only genomes with completeness > 99% according to CheckM and they were saved in [keys_best_asm.tsv](https://webfs/n/projects/jp2992/MOLNG4331/flye/pan-genome_analysis/MAG_genomes/keys_best_asm.tsv) . **It was retained 77 out of 89 MAG genomes**.


# Antecedents
****

I tried to use some tools coupled with the plasmid dataset with 114 sequences built before. However, they did not performed as expected for these reasons:

1. **Mob_recon**: depends on the database to retrieved a plasmid. Several plasmids for this bacterias have not been reported such as mag215 (this changed, they released the complete genome some days ago!!) and without markers such as OriT, MPF and Relaxases the identification depends on BLASTn and circularization.
2. **Sourmash**: basically chromosomes and super-plasmids can share hashes with the accessory plasmids so this strategy would need much custom code to try to remove the chromosome and the super plasmids (especially the latter).
3. **Plasmer**: It predicts chunks of them as plasmids. I know which peaces are accessory plasmid by mapping the Illumina version to the PacBio version. For illumina mag215 it predicted 41 sequences for a total of 3,119,688 bp.  The problem is that is was trained in the whole PLSDB which includes mega-plasmids.
4. **PLASMe**: Another machine learning tool for plasmid prediction, it as trained using genomic features using chromosomes and the PLSDB, but they filtered the latter <500kb which is what I needed, It first align contigs with BLAST and filter cov.&id.>90% to reference plasmids and then predicts the reminder using protein cluster formed with the same database using BLASTP and MCL, however it does not work as expected. It failed to correctly predict mag215.
5. **RFPlasmid:** Similar to Plasmer with limitations because of the dataset used to train, but I could use it to train my own model.

# Methods
****

Given the strategies before did not work and considering that we do not have too much genomes, I will try to use alignment (BLAST or Minimap2) to retrieve unique sequences coupled with typing with MOB-Suite. 

**I decided to use minimap2** because I consider it is easier to run and parse the output. Additionally, it can be tolerant to SV producing kind of glocal alignments and it also computes the *Gap-compressed per-base sequence divergence* (de:f) which could help for identity assessment for sequences that might have indels due to changes in gene content. I will align to the chromosomes and super-plasmids downloaded from complete genomes to try to do the opposite to before, **instead of retrieving the accessory plasmids I will remove everything that is in the chromosomes and the super-plasmids.** 

To do so, I've had to fine-tune thresholds. Now, I will describe the thresholds taken into account:

1. **Identity:** For this I am using de:f from minimap2. I like this metric because it will be permissive with gene indels. **I set it for <0.1, so 90% identity.**

2. **Query cover:** Given that this is Illumina we can have cases where the gene indel is at the beginning or end of the read. I have noticed that between the super-plasmids the changes can be enormous >10kb for example:
	* [example_variable_psymA.png](https://webfs/n/projects/jp2992/stowers-notes/photos/example_diff_psymA.png)
	* We can see that using a cov >90%, this giant contig that belongs to the super-plasmids is discarded because the best reference for it is lacking 39kb at the beginning and 10kb at the end. resulting in a query coverage of 89%.

**Therefore, I decided that a query cov. > 90 %  for aligned fragments 2kb< x < 50 kb. For x>50kb only identity is taken into account**.  

The filter mentioned are applied through this custom script: [paf_parse.py](https://webfs/n/projects/jp2992/MOLNG4331/code/paf_parse.py)

> [!NOTE]
> **This strategy will not reconstruct the accessory plasmids**, but, as long as we have enough reference genomes, it will tell us unique accessory peaces. **The real problem is the super plasmids, like psymA.** It carries accessory genes or genomic islands. ***How can we differentiate an accessory gene coming from psymA or the accessory plasmid?***
> 

The presence of accessory genes provided by an accessory plasmid can be confirmed with plasmid proteins predictions, for example, relaxases, MPF and replicons by ***Mob-typer***. All genomes having more than 2 relaxases matches might indicate the presence of accessory plasmids.

Mob-typer uses BLASTn which can be sensible to divergence, so the output presenting the biomarker matching can produce redundant matches, a custom script ([parse_mob_suite.py](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/plasmid_recon/parse_mob_suite.py)) was used to clean it. The script only organizes the output by biomarker, length and ID, and removes duplicates, so at the end we get the count of unique matches. 

**There are some sequences with less than 2 relaxases predictions.** I need a different clue to hunt for acce. plasmid:
	- I will try to see percentage of similarity of RepABC, it is apparently conserved in the accessory plasmids, how different it is from the super-plasmids???
		-  **My preliminary observations** say that RepABC differ significantly between accessory plasmids and mega-plamids. However, for example in mega plasmid I have found RepA duplication with significant identity divergence. **Therefore, I can only count on finding RepABC in the same contig.**
	- I saw that it can happen that relaxases were zero, however it still found the MPF, but I cannot use number of MPF machinery as some accessory plasmids can have it, so I cannot difference between psymA/B and accessory. Additionally, this comprises repetitions that very likely will be hard for most Illumina assemblies. 
	- I missed a fact that can help determined presence of accessory plasmids. I have noticed that **most of the time PsymA/B only present MOBQ relaxases**, accessory plasmids can also present it, but they can also present MOBP.


# First Result: prediction by alignment and classic typing
****

## Last minute updates

Some MAG genomes were sequenced for the paper: *Mobile gene clusters and coexpressed plant–rhizobium pathways drive partner quality variation in symbiosis*

| Accession       | Strain   |     | Table | Acc. plasmid |
| --------------- | -------- | --- | ----- | ------------ |
| GCA_033715235.1 | 121      |     |       | No           |
| GCA_033715505.1 | **144B** |     | 1     | Yes          |
| GCA_033715655.1 | 182      |     |       | No           |
| GCA_033713625.1 | 199      |     |       | No           |
| GCA_033713685.1 | **204**  |     | 2     | Yes          |
| GCA_033715695.1 | 230      |     |       | Yes          |
| GCA_033713955.1 | **278**  |     | 4     | Yes          |
| GCA_033713415.1 | 31       |     |       | No           |
| GCA_033716245.1 | **746B** |     | 2     | Yes          |
|                 |          |     |       |              |

The *table* column shows which of the tables below presented these strains and the *Acc. Plasmid* column shows if they present accessory plasmid. For example, MAG230 was among our MAG collection and it has an acc. pls, but it was not predicted to have acc. pls. 

However some strains were not found in our MAG dataset:

| Strain | Acc. plasmid |
| ------ | ------------ |
| 748B   | No           |
| 176A   | No           |
| 724B   | No           |
| 335    | No           |
| 89     | No           |
| 141    | No           |
| 25B    | Yes          |
| 206    | Yes          |
| 278    | Yes          |


## More than 2 relaxases

[more_than_2_relaxases_genomes](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/plasmid_recon/more_than_2_relaxases_genomes/) contains all the genomes that presents 3 o more relaxes in different contigs.

**With this strategy 20 out of 77 MAG draft genomes contains an accessory plasmid.** However, it is worth reviewing the other 57 genomes as some of them where predicted with less than 2 relaxases, and even worthy to check the ones with only 2 relaxases, as this strategy depends on the correct assembly and BLASTn (mob-typer) to a general relaxases database.                      

| file                                 | strain   | num_seqs | sum_len | min_len | avg_len  | max_len | relaxase | replicon |
| ------------------------------------ | -------- | -------- | ------- | ------- | -------- | ------- | -------- | -------- |
| putative_plasmid_GCA_033712485.fasta | **18**   | 24       | 505,236 | 2,006   | 21,051.5 | 73,858  | 3        | 1        |
| putative_plasmid_GCA_033712675.fasta | 24       | 6        | 267,376 | 2,562   | 44,562.7 | 93,639  | 3        | 1        |
| putative_plasmid_GCA_033713265.fasta | 27       | 7        | 273,086 | 2,218   | 39,012.3 | 102,346 | 3        | 1        |
| putative_plasmid_GCA_033713405.fasta | 40       | 16       | 282,804 | 4,892   | 17,675.3 | 49,106  | 5        | 1        |
| putative_plasmid_GCA_033713615.fasta | 200      | 6        | 277,840 | 17,260  | 46,306.7 | 111,404 | 3        | 0        |
| putative_plasmid_GCA_033713795.fasta | 221      | 3        | 206,176 | 32,076  | 68,725.3 | 114,138 | 3        | 1        |
| putative_plasmid_GCA_033713875.fasta | 245      | 7        | 261,605 | 3,365   | 37,372.1 | 78,980  | 3        | 2        |
| putative_plasmid_GCA_033714075.fasta | 342      | 22       | 514,302 | 3,468   | 23,377.4 | 87,195  | 4        | 4        |
| putative_plasmid_GCA_033714785.fasta | 755A     | 33       | 450,886 | 2,206   | 13,663.2 | 55,621  | 4        | 2        |
| putative_plasmid_GCA_033715505.fasta | **144B** | 16       | 219,960 | 2,026   | 13,747.5 | 40,495  | 3        | 1        |
| putative_plasmid_GCA_033715555.fasta | 169      | 20       | 408,131 | 2,037   | 20,406.6 | 102,600 | 3        | 1        |
| putative_plasmid_GCA_033715635.fasta | **177**  | 6        | 314,947 | 5,298   | 52,491.2 | 181,012 | 3        | 1        |
| putative_plasmid_GCA_033715675.fasta | **215**  | 5        | 169,932 | 5,584   | 33,986.4 | 92,903  | 3        | 1        |
| putative_plasmid_GCA_033716305.fasta | 748A*    | 8        | 271,280 | 10,127  | 33,910   | 57,568  | 3        | 2        |
| putative_plasmid_GCA_033716455.fasta | 154      | 20       | 352,075 | 2,050   | 17,603.8 | 68,908  | 4        | 1        |
| putative_plasmid_GCA_033716465.fasta | 192D     | 6        | 231,540 | 19,832  | 38,590   | 59,219  | 3        | 0        |
| putative_plasmid_GCA_033716485.fasta | 184      | 6        | 187,067 | 8,268   | 31,177.8 | 60,240  | 3        | 2        |
| putative_plasmid_GCA_033716575.fasta | 248      | 6        | 151,972 | 10,594  | 25,328.7 | 68,747  | 3        | 1        |
| putative_plasmid_GCA_033716795.fasta | 97       | 15       | 418,557 | 6,111   | 27,903.8 | 102,600 | 3        | 1        |
| putative_plasmid_GCA_033716825.fasta | 123      | 6        | 182,077 | 10,891  | 30,346.2 | 52,128  | 3        | 1        |


**In bold** we see the in-house strains sequenced with PacBio that presented an accessory plasmid.

\* It did not present accessory plasmid according to sam.

> [!UPDATE]
> 
> After prediction, Samantha found "that **only MAG748A did not have one**. MAG18, MAG97, and MAG342 all had two accessory plasmids, and the rest had one."

## Only 2 or Less relaxases 

> [!NOTE]
> 
> This strategy presents a big flaw. The supposition that MOBP was only found in accessory plasmids turned out to be false. I found some PsymA carrying MOBP due to possibly Integrative Mobile Elements (IME). 
>     


I used mob-typer to know the genomes that have 3 or more relaxases and I mapped to the chromosomes, and super-plasmids to get the unmapped sequences as putative accessory plasmids sequences (check Methods).

Therefore, for this dataset the first filter will be to get those presenting a MOBP. Additionally, I added the best match in the PLSDB database, if any.

Consider that I took the whole file as one plasmid (it might contains Psyms leaks)


| Code          | strain   | file                                 | num_seqs | sum_len | min_len | Mean Len | Max Len | refSeq        | Hash_dist | shared_hashes |
| ------------- | -------- | ------------------------------------ | -------- | ------: | ------- | -------- | ------: | ------------- | --------- | ------------- |
| GCA_033713685 | **204**  | putative_plasmid_GCA_033713685.fasta | 9        |  191985 | 2474    | 21331.7  |   62808 | NZ_MZ505104.1 | 0.0712856 | 126/1000      |
| GCA_033715315 | 701B     | putative_plasmid_GCA_033715315.fasta | 4        |  127694 | 2255    | 31923.5  |  111857 | CP140912.1    | 0.0943778 | 74/1000       |
| GCA_033715825 | 258      | putative_plasmid_GCA_033715825.fasta | 19       |  368402 | 2673    | 19389.6  |   59396 | CP140885.1    | 0.0680698 | 136/1000      |
| GCA_033715995 | 513      | putative_plasmid_GCA_033715995.fasta | 15       |  198921 | 2454    | 13261.4  |   52061 | NZ_CP148088.1 | 0.0751681 | 115/1000      |
| GCA_033716245 | **746B** | putative_plasmid_GCA_033716245.fasta | 2        |  198401 | 85699   | 99200.5  |  112702 | NZ_CP140898.1 | 0.0404475 | 272/1000      |
| GCA_033716625 | 322      | putative_plasmid_GCA_033716625.fasta | 17       |  345338 | 2021    | 20314.0  |   74881 | —             | —         | —             |
| GCA_033713835 | 225      | putative_plasmid_GCA_033713835.fasta | 11       |  304754 | 3920    | 27704.9  |   62398 | —             | —         | —             |
| GCA_033714135 | 373      | putative_plasmid_GCA_033714135.fasta | 12       |  246973 | 4060    | 20581.1  |   62557 | —             | —         | —             |
| GCA_033714725 | 749C     | putative_plasmid_GCA_033714725.fasta | 20       |  323094 | 2034    | 16154.7  |   67112 | —             | —         | —             |
| GCA_033716105 | 539      | putative_plasmid_GCA_033716105.fasta | 20       |  313710 | 2037    | 15685.5  |   72929 | —             | —         | —             |
| GCA_033716535 | 242      | putative_plasmid_GCA_033716535.fasta | 12       |  304849 | 6411    | 25404.1  |   50349 | —             | —         | —             |
| GCA_033716835 | 145      | putative_plasmid_GCA_033716835.fasta | 17       |  394841 | 2158    | 23225.9  |   92312 | —             | —         | —             |
|               |          |                                      |          |         |         |          |         |               |           |               |


**Total strains retrieved: 12**

Now, for the rest of them I only considered a match with the PLSDB. Therefore, they represent a more suspicious result. You will find the best :

| refseq        | file                | strain  | contig         | hash_dist | shared_hashes | length | gc    |
| ------------- | ------------------- | ------- | -------------- | --------- | ------------- | ------ | ----- |
| NZ_CP149882.1 | GCA_033713955.fasta | **278** | WOJC01000028.1 | 0.0579033 | 174/1000      | 94490  | 57.72 |
| NZ_CP085526.1 | GCA_033713975.fasta | 286*    | WOJE01000030.1 | 0.0955937 | 72/1000       | 64831  | 61.71 |
| NZ_CP021811.1 | GCA_033713975.fasta | 286*    | WOJE01000040.1 | 0.0909306 | 80/1000       | 51176  | 59.17 |
| CP140923.1    | GCA_033714485.fasta | 722B    | WOJT01000041.1 | 0.0893096 | 83/1000       | 54825  | 58.10 |
| NZ_CP021817.1 | GCA_033714485.fasta | 722B    | WOJT01000063.1 | 0.0680698 | 136/1000      | 20861  | 63.26 |
| NZ_MZ505104.1 | GCA_033716055.fasta | 514     | WOLU01000066.1 | 0.0310744 | 352/1000      | 11753  | 56.27 |
| NZ_MZ505104.1 | GCA_033716055.fasta | 514     | WOLU01000068.1 | 0.0391011 | 282/1000      | 10689  | 58.67 |
| NZ_MZ505104.1 | GCA_033716055.fasta | 514     | WOLU01000071.1 | 0.0491    | 217/1000      | 7885   | 58.97 |
| NZ_CP021796.1 | GCA_033712725.fasta | 41*     | WOHN01000041.1 | 0.0759181 | 113/1000      | 45812  | 62.25 |
| NZ_CP148087.1 | GCA_033715935.fasta | 406*    | WOLQ01000048.1 | 0.0696435 | 131/1000      | 30143  | 58.25 |
| NZ_CP140902.1 | GCA_033715935.fasta | 406*    | WOLQ01000051.1 | 0.0909306 | 80/1000       | 24057  | 56.54 |
|               |                     |         |                |           |               |        |       |
|               |                     |         |                |           |               |        |       |

**Total strains retrieved: 6**
\* Do not have acc. pls according to Samantha's results

Considering all I retrieved 18 strains out of the 57 that were left previously after the first prediction.



A total of 38 out of 77 strains used were covered by one of the processes above, however, there are other 39 to evaluate. From those a total of 31 presented "unique" fragments (11 did not)

Results for collaborator strains and MAG strains were mixed in this excel sheet: [reassembled_pls_final_w_strains_keys.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/flye_asm/stats_putative_pls/reassembled_pls_final_w_strains_keys.xlsx "https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/flye_asm/stats_putative_pls/reassembled_pls_final_w_strains_keys.xlsx")

Samantha's result showed that filters before for liana's assembly (pacbio) were not that strict so I was re-evaluated. I am now using RFPlamid which is a model I trained on S. meliloti (check below).



After Samantha ran some of these in Gel a list was created in [List of plasmids to re sequence.md](https://webfs/n/projects/jp2992/stowers-notes/List%20of%20plasmids%20to%20re-sequence.md) 



# Second Result: predictio by machine-learning based methods

Different tools were tried. RFPlasmids worked the best. However, it did not present results super impacting, specially because the scores between plasmids and chromosome are not very helpful in many cases. 

## Prediction with MGE-Cluster

The problem with this strategy is that new plasmids different enough will be unclassified based on a clustering model. Additionally, this strategy presents problem for fragmented contigs like the Illumina ones, as those contigs belonging to psym that shared big genomic regions with accessory plasmids are misclassified as plasmids. I tried treating all the unique sequences as one sequence as well as each sequences as one plasmid.


## Prediction with PLASMe

Despite the fact the authors filtered the PLSDB as I needed it x<350kb, it first remove plasmids sequences with strict BLASTN (cov&id > 0.9) and then it predicts the reminder with transformer models, but given the contigs share so many sequences, it happens the same as with MGE-Cluster, misclassifying them as plasmids. 
 

## Prediction with RFPlasmid

This tools allow me to train a random forest model from chromosomes and plasmids. apparently I need at least 20 sequences of each and draft genomes are recommended.

This most laborious part here is that i need to establish a very good dataset. 

### Training dataset
For the chromosome I can use:
1. The complete sequences > 800kb in the NCBI.
2. The MAG draft genomes confirmed by sam.
3. The MAG confirmed by in-house PacBio (A02_asm_hifiasm.fasta, C01_asm_flye.fasta, D01_asm_flye.fasta, F01_asm_flye.fasta)
4. 

To determine draft sequences for acce. plasmids is harder. How will I get complete unique sequences of unknown accessory plasmids? 

Therefore for plasmids I used all complete plasmids for Sinorhizobium below 500kb. 

### Testing dataset
I will use these draft genomes as my negative control test dataset:

| Accession       | MAG-Strain |
| --------------- | ---------- |
| GCA_033715235.1 | 121        |
| GCA_033715655.1 | 182        |
| GCA_033713625.1 | 199        |
| GCA_033715695.1 | 230        |
| GCA_033713415.1 | 31         |

I will use this as my positive control test dataset all the predicted at the beginning of this document (n=20) where Samantha confirmed 19.
 

From the 30 strains that remained unpredicted from the first result. **A total of 16 more were retrieved** according to their plasmids predictions. 




# Final file

All the predicted strains using both methods were saved in a spreadsheet for sequencing [list_strains_w_pls_to_sequencing_copy_for_siva.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/plasmid_recon/list_strains_w_pls_to_sequencing_copy_for_siva.xlsx) 

I removed strains with no plasmids confirmed by Samantha and strains with a complete genome in the NCBI.

