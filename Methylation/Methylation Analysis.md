
> [!NOTE]
> During methylation calling some problems arise with the the pi and pw tags. This problem is only if you are running methylation calling in command line, since during microbial analysis SMRT Link using GUI they applied this solution. Refer to this [document](https://webfs/n/projects/jp2992/stowers-notes/Methylation%20Calling%20PacBio%20HiFi.md) to avoid the pain in the ass. Remember you need FI,RP,FP


# Antecedents 


* In this study [DNA Methylation in _Ensifer_ Species during Free-Living Growth and during Nitrogen-Fixing Symbiosis with _Medicago_ spp.](https://journals.asm.org/doi/10.1128/msystems.01092-21) authors found interesting methylation changes in GANTC motif recognized by CcrM, a methytransferase proved to be cell cycle regulated in C. crescentus and A. tumefaciens. They found that only the GANTC was methylated in all strains. In actively dividing cell cultures, methylation of GANTC motifs increased progressively from the _ori_ to _ter_ regions in each replicon, in agreement with a cell cycle-dependent regulation of CcrM. **In contrast, there was near full genome-wide GANTC methylation in the early stage of symbiotic differentiation**. This was followed by a moderate decrease in the overall extent of methylation and a progressive decrease in chromosomal GANTC methylation from the _ori_ to _ter_ regions in later stages of differentiation.
	* What I question:
		> "Based on gene annotations, we identified 24 genes encoding putative MTases in a previous pangenome analysis of 20 _E. meliloti_ strains (Table S1 at [https://doi.org/10.6084/m9.figshare.16556205](https://doi.org/10.6084/m9.figshare.16556205))" <span style="color: red">How did they searched for these proteins?</span> they referenced this [study](https://cdnsciencepub.com/doi/full/10.1139/cjm-2018-0377#sec-3), however the study only showed the pan-genome construction with Roary. 
	 
	* This part is key
		* Unlike _B. diazoefficiens_ USDA110 (38), we did not identify motifs that were methylated specifically in the _E. meliloti_ bacteroids. In addition, we found little evidence for any of the methylated motifs being enriched in the promoter regions of _E. meliloti_ Rm2011 genes up-regulated or down-regulated in bacteroids relative to free-living cells, as identified in published transcriptomic data for _E. meliloti_ Rm1021 ([23](https://journals.asm.org/doi/10.1128/msystems.01092-21#core-collateral-B23)). These data suggest that most DNA methylation is unlikely to be a significant factor in directly regulating gene expression in _E. meliloti_ bacteroids.
		* GANTC is the exception.
	
![[meth_motif_s_meliloti.png]]

* This interesting study: [The Complex Epigenetic Panorama in the Multipartite Genome of (...) Sinorhizobium meliloti](https://doi.org/10.1093/gbe/evae245) presented the *methylome* (6mA and 4mC) of S. meliloti and the found some *core* and *disposable* methylation-target motif. I gathered the motifs in a [spreadsheet](https://webfs/n/projects/jp2992/MOLNG4331/methylation_analysis/#:~:text=methylation_motifs_pan%2Depigenome_paper.xlsx) 

* They also created a software [MeStudio](https://github.com/combogenomics/MeStudio) to "analyze and combine genome-wide methylation profiles with genomic features." However, it does not work and they do not provide support.


# Data


My interest is to inspect how methylation pattern looks like compared to the WT (1021). 

So, as of Oct-2025, I will be using the same data assembled in [Project-report-cbio.mm2883.102.html](https://webfs/n/projects/jp2992/Stowers-notes/Project-report-cbio.mm2883.102.html) 


# Benchmarking: Nanopore vs PacBio


> [!NOTE]
> **The PacBio of B. japonicum does not have the kinetic tags :(** it makes sense considering it is not from an in-house sequencing. Therefore, I do not think we can get them as if they are not present in the BAM they are lost. 
> 

To start a project on this. First, we have to decide which tool is better for detecting methylation 6mA and 4mC. 

Nanopore is a interesting option because it has very good models for 6mA and 4mC detecting as well as a good community-maintained toolkit for modification exploration. However, Nanopore is not famous by their DNA quality. On the other hand PacBio has very good quality and detection of 4mC and 6mA as well. However, they tools for modification processing are old and poorly developed. Additionally, in the past it was reported that PacBio was not very accurate at GpG islands during 5mC detection, however, it was recently improved using neural networks (ccsmeth). However, the same advances has not been reported in m4C. (6mA is good). Nonetheless, Nanopore has been reported as more sensible than PacBio in this aspect. 

Therefore, will perform a comparison using 30x, 50x and 100x depths between Nanopore and PacBio to see the level of concordance between both tools and uniqueness. 

# Benchmarking 2.0

Given that the comparison was not possible as I do not have tags. I can try to make a comparison between the motifs found in free living B. japonicum with Nanopore and the results in this [paper](https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2016.00518/full) which used PacBio.

These are the motifs found for free living B. japonicum during the mentioned study:

![[motifs_pacbio_b_japonicum.png]]

Using Nanopore, I found a genome with the following coverage stats:

| seq_name | length  | cov. | circ. |
| -------- | ------- | ---- | ----- |
| contig_4 | 9107642 | 691  | Y     |
| contig_1 | 3513467 | 323  | Y     |
| contig_3 | 273713  | 476  | Y     |
| contig_2 | 269090  | 411  | Y     |
| contig_6 | 139450  | 171  | Y     |
| contig_7 | 25600   | 127  | Y     |
| contig_5 | 22479   | 1206 | Y     |

Noticed the contamination. However, B. japonicum is easily retrieved by size. We got then a 9Mb genome with 691 mean coverage.

Using the full data Modkit report the following motifs:

| mod_code | motif         | offset | frac_mod  | high_count | low_count | mid_count |
| -------- | ------------- | ------ | --------- | ---------- | --------- | --------- |
| a        | GAGANNNNNNRTG | 3      | 1         | 2066       | 0         | 14        |
| a        | CRAGGAT       | 5      | 1         | 4004       | 0         | 2         |
| a        | CAYNNNNNNTCTC | 1      | 1         | 2079       | 0         | 1         |
| a        | GANTC         | 1      | 0.9990239 | 31728      | 31        | 1416      |

Noticed that there is a 4mC motif missing. This is because this motif is shared with a 6mA modification. I am not sure if it does not appear because of the masking with 6mA or because its occurrence is very low. Check the stats for reads > 500bp and probability >80%:

| base  | code      | pass_count | pass_frac        | all_count | all_frac         |
| ----- | --------- | ---------- | ---------------- | --------- | ---------------- |
| C     | -         | 10355303   | 0.9992905        | 10536716  | 0.99626136       |
| C     | m         | 779        | 0.00007517378    | 3823      | 0.00036147004    |
| **C** | **21839** | **6573**   | **0.0006342969** | **35718** | **0.0033771873** |
| A     | -         | 5967067    | 0.9788003        | 7101249   | 0.9539235        |
| A     | a         | 129240     | 0.02119972       | 343005    | 0.046076477      |

In bold we can see that it is detected but its numbers are low.


Using 3 different coverages, 30x,50x and 100x I saw no significant difference:

| motif         | offset | cov | frac_mod  | high_count | low_count | mid_count |
| ------------- | ------ | --- | --------- | ---------- | --------- | --------- |
| GAGANNNNNNRTG | 3      | 100 | 1.0000000 | 2062       | 0         | 18        |
| GAGANNNNNNRTG | 3      | 30  | 0.9995141 | 2057       | 1         | 22        |
| GAGANNNNNNRTG | 3      | 50  | 0.9995136 | 2055       | 1         | 24        |
| CRAGGAT       | 5      | 100 | 1.0000000 | 4004       | 0         | 2         |
| CRAGGAT       | 5      | 30  | 1.0000000 | 4004       | 0         | 2         |
| CRAGGAT       | 5      | 50  | 1.0000000 | 4004       | 0         | 2         |
| CAYNNNNNNTCTC | 1      | 100 | 1.0000000 | 2079       | 0         | 1         |
| CAYNNNNNNTCTC | 1      | 30  | 1.0000000 | 2079       | 0         | 1         |
| CAYNNNNNNTCTC | 1      | 50  | 1.0000000 | 2079       | 0         | 1         |
| GANTC         | 1      | 100 | 0.9989190 | 31418      | 34        | 1723      |
| GANTC         | 1      | 30  | 0.9982884 | 30330      | 52        | 2787      |
| GANTC         | 1      | 50  | 0.9988049 | 30922      | 37        | 2216      |


# Problems with data processing

Here, I describe the tools I tried to analyze and combine genome-wide methylation profiles with genomic features: 

1. **MeStudio:** It does not work. Not by problems with processing, but due to bugs in the code. I suspicious that since the authors are not providing support it is an old code. Since there explicit bugs such as inconsistencies with the tools flags. I tried to fix them but it has much problems.
2. **Bacmethy:** It was designed to handle only one contig. Additionally, it needs prokka format annotation. 
	1. **Solutions tried:**
	
		1. **handle each contig separately** This was the initial approach. The problem is that it is a pain to match this with the RNA-seq mapping. As because they present separate annotation I have the risk of duplicates and if I fix the duplicates I have to fix it for Bacmethy as well.
		
		2. **Handle each contig separately and copy a common annotation** Bamethy does not care about file names, just the folder name. So i copied the prokka annotation into each contig's folder. What i fear is that because everything in this damn tools is hardcoded then I does not consider that the annotation presents different contigs. Inside the prokka folder, according to the code, Bacmethy is supposed to take three files `*.fna *.gff *.tsv` therefore I had to change the `*.fna` file as well. **However**, it presents problems when doing the intersection with BEDtools.

3. **DNAModAnnot** (R package) 

# Methylation stats

