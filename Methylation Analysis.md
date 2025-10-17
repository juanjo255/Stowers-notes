
> [!NOTE]
> During methylation calling some problems arise with the the pi and pw tags. This problem is only if you are running this in command line, since during microbial analysis SMRT Link, they applied the solution. Refer to this [document](https://webfs/n/projects/jp2992/stowers-notes/Methylation%20Calling%20PacBio%20HiFi.md) to avoid the pain in the ass.


# Antecedents 


* In this study [DNA Methylation in _Ensifer_ Species during Free-Living Growth and during Nitrogen-Fixing Symbiosis with _Medicago_ spp.](https://journals.asm.org/doi/10.1128/msystems.01092-21) authors found interesting methylation changes in GANTC motif recognized by CcrM, a methytransferase proved to be cell cycle regulated in C. crescentus and A. tumefaciens. They found that only the GANTC was methylated in all strains. In actively dividing cell cultures, methylation of GANTC motifs increased progressively from the _ori_ to _ter_ regions in each replicon, in agreement with a cell cycle-dependent regulation of CcrM. **In contrast, there was near full genome-wide GANTC methylation in the early stage of symbiotic differentiation**. This was followed by a moderate decrease in the overall extent of methylation and a progressive decrease in chromosomal GANTC methylation from the _ori_ to _ter_ regions in later stages of differentiation.
	* What I question:
		> "Based on gene annotations, we identified 24 genes encoding putative MTases in a previous pangenome analysis of 20 _E. meliloti_ strains (Table S1 at [https://doi.org/10.6084/m9.figshare.16556205](https://doi.org/10.6084/m9.figshare.16556205))" <span style="color: red">How did they searched for these proteins?</span> they referenced this [study](https://cdnsciencepub.com/doi/full/10.1139/cjm-2018-0377#sec-3, however the study only showed the pan-genome construction with Roary. 
	 
	* This part is key
		* Unlike _B. diazoefficiens_ USDA110 (38), we did not identify motifs that were methylated specifically in the _E. meliloti_ bacteroids. In addition, we found little evidence for any of the methylated motifs being enriched in the promoter regions of _E. meliloti_ Rm2011 genes upregulated or downregulated in bacteroids relative to free-living cells, as identified in published transcriptomic data for _E. meliloti_ Rm1021 ([23](https://journals.asm.org/doi/10.1128/msystems.01092-21#core-collateral-B23)). These data suggest that most DNA methylation is unlikely to be a significant factor in directly regulating gene expression in _E. meliloti_ bacteroids.
		* GANTC is the exception.
	
![[Screenshot 2025-10-17 at 9.08.45 AM.png]]
* This interesting study: [The Complex Epigenetic Panorama in the Multipartite Genome of [...] Sinorhizobium meliloti](https://doi.org/10.1093/gbe/evae245) presented the *methylome* (6mA and 4mC) of S. meliloti and the found some *core* and *disposable* methylation-target motif. I gathered the motifs in a [spreadsheet](https://webfs/n/projects/jp2992/MOLNG4331/methylation_analysis/#:~:text=methylation_motifs_pan%2Depigenome_paper.xlsx) 

* They also created a software [MeStudio](https://github.com/combogenomics/MeStudio) to "analyse and combine genome-wide methylation profiles with genomic features." 


# Data


My interest is to inspect how methylation pattern looks like compared to the WT (1021). 

So, as of Oct-2025, I will be using the same data assembled in [Project-report-cbio.mm2883.102.html](https://webfs/n/projects/jp2992/Stowers-notes/Project-report-cbio.mm2883.102.html) 


# Methylation stats

