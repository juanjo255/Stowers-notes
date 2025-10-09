
# To Do (weekly)

- [x] Get 16S from microbiome
- [ ] Cluster plasmids from strains dakota and penn. 
	- [ ] Diversity of plasmids: how similar.
- [ ] Methylation profile differences between rm1021 and mag215 
 
- [ ] Build a genome map of annotation for accessory plasmids:
	- The idea is to show an artificial genome built by the plasmids. 
- [ ] Add the MAG strains ours and the ncbi published to the clustering.
- [ ] Highlight all the clusters where the new plasmids fall.
- [ ] Make homology network colored by the clusters of MGE-Cluster and highlight the new plasmids.


- [x] Look for taurine cluster in S. meliloti in other:
	-   The taurine cluster in S. Meliloti 1021 is located in PsymB:
		- SM_b21526 (tauA)
		- SM_b21527 (tauB)
		- SM_b21528 (tauC)
		- SM_b21529 (tauD)

- [ ] Check dakota collaborator assemblies:
	-  **TO NOTE:** I assembled using the pipeline Hybracter. It assemblies with Flye and includes Plassembler to get plasmids. A small comparison shows me that **Flye reported 54 samples** containing sequences below 500kb being circular, however **Plassembler recovered only in 18 of them**. One reason for this could be that Plassembler is actually sensible to coverage when using only long reads (maybe because of Unicycler? anyways its main purpose is to be used with hybrid assemblies). For example, 
		<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/flye_asm_P9A10.png" height=300 > 
		In the picture the helicopter propeller is probably the two psymA/B and there are apparently two circular acce. plasmids

		<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/plassembler_asm_P9A10.png" height=400 > 
		Plassembler in this case reported no circular plasmids.  

- [ ] Add in house plasmids to MGE-Cluster to see how they relate with other plasmids.

- [ ] Cluster all retrieved accessory plasmids:
	- [x] Collect all the genus reported for nodule in M. sativa and M. truncatula
	- [ ] Repeat clustering process below and homology network with the plasmids captured from other genus
	- [ ] Using all the plasmids for the core genus in nodule PLSDB it was only 2,345 sequences too much for mge-cluster, I do not want to imagine COPLA).
	- [x] Using only accessory plasmids.
	- [ ] Cluster only sinorhizobium (including mega-plasmids) to see if we can differentiate between mega and accessory plasmids with this strategy. 
	
- [ ] Plot homology network using same plasmids used before.
	- [x] For this I am using the code from a study (check plasmidome report  and jupyter Notebook) and plotting network graph of how are plasmids related in terms of homology measured by wGRR. 
	- This can helps us to check for recombinant genes using metrics wGRR< 0.1 and BHH 80-80 inspired by the paper of phages-plasmids.

- [ ] RNA-seq proccessing.
	- [ ] So far, mapping 215 to 1021 do not show differential expressed genes.

- [ ] Build a Pan-genome graph for S. meliloti using susceptible strains. I have to wait for Madi info.
	- [ ] I received the susceptible MAG from Madi on Jul. 14. [resistant_strains.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/resistant_strains.xlsx)
	- [ ] PPanGGoLin for pan-genome construction. *Update:* Its faster than Roary, it has support and plenty of several stats and graphs.
	- [ ] Try minigraph-cactus as an alternative to progressiveMauve since I do not like the output of it. it also allows to create pan-genome graph.
 - [ ] **Improve annotation for genes:** I missed the use of tools like InterProScan.
	- During a meeting Eric Ross and Sukha Malladi annotate using their pipeline intended for eukaryotes, but has some tools useful for bacteria like interproscan, nonetheless they did not find significant matches for hypothetical proteins.

Future:
- [ ] Pan-genome of everything.
- [ ] Annotate SNPs using DeepVariant or Clair3.

# Take into account for future
* In the context of plasmids recovery: 

	* **MGE cluster achieve a peak of a little over 300 Gb using 1,775 plasmids below 500kb**. Including the mega-plamids (fora. total of 2,345 ) is not enough with 600 Gb of memory!!
	* **PsymA can carry MOBP.** 
		* I usually find MOBQ in psymA/B, however m64404e_240423_150118.hifi_reads.bc2003--bc2003 show me that PsymA can have a MOBP possibly by a genomic island. For example, after checking the PLSDB I found for plasmids greater than 500kb: MOBP: 3, MOBQ: 99. 
	* **Check Plasmidome document for tools tried.**
	* **Low coverage fragment the chromosome and entangles PsymA**.
		* The low coverage cause in Flye two interesting problems: 1, It fragments genomes by repetition, and 2, It mixes accessory plasmid and mega-plasmid by conserved proteins (MPF). Hifiasm was bolder, it miss-assembles mega-plasmid and accessory plasmids. Check section of collaborator assembly.
	* **MOB proteins predicted in PLSDB for mega-plasmids.**
		* **Plasmids greater than 500kb:**
			-  MOBP: 3
			-  MOBQ: 99 
		- **Plasmids lower than 500kb:**
			- MOBV: 1
			- MOBQ: 42
			- MOBP: 19
	* **Regarding the protein vs protein comparison between KH35cA and pMAG215.** They are very divergent, a mmseqs2 comparison or BLASTP is no enough to get all the homologous. Here an example:
		- Both plasmids were annotated for *S. meliloti* RepABC, however only RepA/C are clustered under thresholds for 80-90% cov and 50-80% id. RepB is very divergent at the point that they are predicted under a different non-redundant sequence assigned to *S. meliloti*. For example, for KH35cA is WP_017272063.1 and for pMAG215 is WP_014989225.1.  I think MMseqs2 offers a possible approach which would involve using an external database this strategy might work as it implies using other sequences that might work better as bait to cluster both of them. But I think it would be too much for only 2 sequences. **Maybe a functional annotation comparison between both would be better?** 
			![[photos/problem_with_RepABC.png]]
	 
* other

# Index of Files

1. [List of plasmids to re-sequence](https://webfs/n/projects/jp2992/stowers-notes/List-of-plasmids-to-re-sequence.md): Taking into account prediction in Plasmidome and collaborators check data here we set a list of plasmids to re-sequence. 



# Done

- [x] **Classify strains in collaborator with acce. plasmids to run on gel**.
	- Among the best plasmids (check report), I will classify the assembled plasmids as super good, intermedia and fishy. 
	- I have to do the same for the illumina MAG strains.
- [x] **Recover plasmids.**
	- I downloaded the last 2024 version of PLSDB database, which is a curated database of plasmid (only complete sequences) here our number of plasmids for meliloti is reduced to 57.  
	- On collab. assemblies.
		- When checking at the biomarkers by mob_suite for all the plasmids in the plsdb, I found the following frequencies for relaxases:
			- **Plasmids greater than 500kb:**
				-  MOBP: 3
				-  MOBQ: 99 
			- **Plasmids lower than 500kb:**
				- MOBV: 1
				- MOBQ: 42
				- MOBP: 19
		- This analysis came up after me thinking that for psymA/B it was always predicted MOPQ and for accessory plasmids I could find MOBP/Q however for example in 2002 if I found a mega-plasmid with no relaxase prediction and one with both MOBPQ/P. 
		- What I want to know is if this can work as a metric to find miss-assembled PsymA/B and putative acce. plasmids. 
- [x] **Define a coverage.** To do this, I will:
	- Define which assembly works better, the collaborator data contains coverage from approx. 10x to 50x very uneven between contigs and with reads sizes two times smaller than ours. ***Update:*** The low coverage cause in flye two interesting problems: 1, fragment genomes by repetition, and 2, mix accessory plasmid and super plasmid by repetition. Hifiasm was bolder, it miss-assembled mega-plasmid and accessory plasmids. Check section of collaborator assembly.
- [x] **Assemble the 121 strains from collaborator.** 
- [x] **For Madi presentation**:
	- [x] Dot plot in house plasmid vs plasmid: https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/homology/all_vs_pmag215/out.pdf
	
	- [x] Matrix accessory genes for plasmids (80% identity): https://webfs/n/projects/jp2992/MOLNG4331/plasmids_smeliloti/roary/roary_result_80_pct/pangenome_matrix.png
	
	- [x] Matrix accessory genes for whole genome (80% identity): https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/roary_result_80_pct_1751912805/pangenome_matrix.png
	- [x] Pie accessory genes for whole genome (80% identity): https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/pan_genome/roary_result_80_pct_1751912805/pangenome_pie.png

	- [x] Dot plot for whole genomes: https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/minimap2/all_vs_mag215_asm20.paf.pdf
	
	- [x] Synteny plot between in-house strains: https://webfs/n/projects/jp2992/MOLNG4331/genomes/genome_comparison/minimap2/plot_synteny/ngenomesyn/prueba.svg
	- [x] Can we find out which of these illumina strains have accessory plasmids and then do PacBio assembles of them?
	- [x] Look into average coverage per assembly, compare to recommended coverage for bacteria, how many samples can we sequence at once and have enough Coverage for assembly?  
	- [x] Run de-novo ORI prediction on all our new plasmids.  

* 30/06/2025 - 09/07/2025
	- [x] Nuclear genome: Process the 8 PacBio resistant strains
		- [x] Check Quality
			- [x] Contiguity 
			- [x] Completeness with CheckM.
			- [x] Descrip. stats with SeqKit.
			- [x] With Flye report I realized A02 assembly has a shared site between the main chromosome and the putative plasmid. The assembler decided to separate them. **I will assemble with Hifiasm**. *Update:* Hifiasm was abled to solved the ambiguity.
		- [x] Genome to genome comparison.
		- [x] Gene presence/absence between all genomes (pan-genome). Get unique genes to MAG215.
	- [x] Accessory plasmids: Process the new plasmids if apply.
		- [x] Typing plasmids with mob suite
			- There is a plasmid non-mobilizable, which casually is the one with weird assembly graph (A02). **meaning that maybe it is not a plasmid but a repetition in the chromosome**.
		- [x] Plasmid to plasmid comparison.
		- [x] Check homology between these plasmids and public plasmids at ncl level.
		- [x] Check homology between these plasmids and MAG215 at ncl level.
		- [x] Roary to get shared genes between in-house plasmids. Get unique genes to pMAg215.
		- [x] I could try check Promer (from MUMmer) to do all-vs-all genome comparison at protein level to check synteny blocks. *Update:* there was no much difference with nucleotide alignment.
		- [ ] 

* 27/06/2025
	- [x]   **Compare accessory plasmid's genes of KH35c and MAG215**.
		- Siva *realized one of our favorite strain KH35c has an accessory plasmid ~180 kb. Some of the genes I was interested in MAG215 are present in this accessary plasmid. Experimentally we see some similar plant phenotype between KH35c and MAG215.*
		- [x] Compare at genome level. *Update:* I used Minimap2 (asm5) and BLAST.
		- [x] Compare at protein level. *Update:* I will use Roary with 80% and 50% of identity and back up with mmseqs2. This because I like the output format of roary but I have more intervention in mmseqs. I set up 90% cov 80% id.

* 26/06/2025
	* I sent Siva report with the alignments of accessory plasmids. 
	* I organized reports
	 * I get vaccinated for hep. B 
	- [x] **Assembly the 8 PacBio resistant strains**
	- [x] Check Quality
	- [ ] Check accessory plasmid in the 8 resistant strains.

* 25/06/2025

	 - [x] **Compare MAG215 with MAG assemblies:** After evaluation with MMseqs2. We decided to try with more closely related strains, apparently MAG215 has diverged significantly. Siva notified that there were some MAG assemblies available from other authors and from which they had information about which ones where susceptible to the peptide. 
		- [x] Adding Rm1021 and Mag215 to the jaccard comparison. *Update:* Rm1021 once again shows not to be the better genome to compare.
		- [x] Compare genome to genome between mag215 and the closest strain. *Update:* QUAST comparison available in the pan-genome report. There is slightly higher coverage in other MAG strains than with Rm1021.  
		- [x] Compare the 89 strains and give Madi the closest  strain to see if they are susceptible. *Update:* Table annotated in pan-genome report.
		- [x] Check if any of the 89 strains have the accessory plasmid from mag215. *Update:* Table available at pan-genome report. The strain with the highest proportion of the plasmid is MAG97. The alignment can be seen in the same QUAST report as before.

* 24/06/2025
	* After the jaccard similarity with sourmash and discussion with Siva and Madi. It looks like the susceptible MAG strains that Madi gave me are still very divergent. I will make a comparison with all 89 MAG strains and will include H01 and B02 to see which of them is the closest.
	- [x] **Run PGAP on our two assembled strains**. *Update:* reduction of genes in B02 (1021) congruent with NCBI annotation.

* 23/06/2025
	* I keep working on MAG strains.
	* Madi gave me only 4. 
	* I was abled to get MAG strains from Daniel
	
* 20/06/2025
	
	- [x] Drop required similarity required to 90% and 80% in Roary - how does that change our rm1021 vs mag215 comparison.
		- **It did not change the result significantly**. I tried 50% and it returned a reduction of 254 genes. 
	- [x] I will inspect the proteins clustering using MMseqs2. As alternate method, I will cluster the both proteomes initially using cov 90% id. 90% as NCBI.
		- I tried 90% coverage and 90%, 80% and 50% identity. **There was a small reduction**. From 90% to 50% there was a reduction of accessory genes of 220.
	
* 18/06/2025
	- [-] I want to try not splitting the paralogs.
		- There was not a big difference in number of group (4 less). As expected the greatest change was with the transposes grouping.
	- [-] Make snippy call first removing the plasmid. This because the plasmid is not part itself of the core genome as the super plasmids always found in smeliloti. 
	
* 17/06/2025
	* I presented result to Andrew, he approved them. 
	* Some things to finish before meeting with Siva: 
		- [-] Proteome comparison between MAG215 and RM1021 using pan-genome strategy with Roary. 
			- [-] Separate files for genes only present in each strain.
			- [-] Table with genes in the plasmid
		- [-] Annotate SNPs in core genome.
			- I used snippy and the core alignment done by Roary and filtered SNPs with snp-sites.
			- I want to annotate the output of snp-sites with genes.

* 16/06/2025
	*  I set up Roary and ran it using RM1021 and MAg215 to do pan-genome analysis. The idea is to check absence/presence of genes between both  and I think I can core alignment in the same tool and characterize variants.
	* I am trying to functionally annotate the extra plasmid using KEGG and GO databases. I am a little tangled with this task. BAKTA supposed to offer grouping by GOG but it did not work I do not the reason. I will try to do this with other tool.

* 13/06/2025
	* I downloaded 753 sequences related with the keywords "Sinorhizobium meliloti[All Fields] AND plasmid[filter]", after I filtered the sequences for all greater than 10kb and lower than 500kb to remove the two big plasmids, the chromosome and genes or cassettes. at the end there were 114 sequences. I found no similar among 75 sequences mapped, only short regions of probably homology. This looks like a new plasmid. The sequences compiled contained also  **pSmeSM11a, pRmeGR4b**. 

* 12/06/2025
	* There are some well described plasmid such as **pSmeSM11a, pRmeGR4b and pTA2** (I did not find the last one in the NCBI).
	* Siva and Medi got 121 new strains we will assemble.

* 11/06/2025
	* Meeting with Dr. Siva finished with some tasks. I will write them in the to do list.
	* QUAST comparison shows that the reference assembly was correctly assembled and the MAG215 might actually carry a high level of divergence. A synteny analysis with ProgressiveMauve indicates that MAG215 (H01) genome might carry acquired and lost particular section from the reference genome, additionally there are not indications of the extra plasmid in the reference genome.

* 10/06/2025
	* I shared advances with my mentor Andrew. While I focused on extra plasmid annotation, he went for assembly vs assembly comparison between the NCBI reference and our strain MAG215 and RM1021 (same strain as NCBI). Also, he did annotation of the genome using LiftOver from NCBI reference to RM1021 as well as to MAG215, however the latter showed around 600 genes were not mapped. He will to do the process backward: annotate MAG215 and liftOver to the reference.
	* There is missing the annotation of VCF for gene context (BEDtools) and the prediction of the effect (SnpEff).

* 09/06/2025
	* **Extra plasmid in H01** (contig_4) apparently is actually a plasmid, relaxes proteins were found and it presents an **interesting hash similarity to an accessory plasmid** in other strain of *S. meliloti* (CP021832). A plasmid matching using **PLSDB** also showed interesting hash matching with other accessory plasmids reported in *S. meliloti*  and *S. medicae* 
	* I annotated with **bakta**, the idea is to see SNPs in CDS. The extra plasmid has a lot of hypothetical proteins, however it seems several of them are annotated as such in the RefSeq.
	* Genome comparison between the GCA genome available at Cerebro with the H01 (MAG215) presents highly divergence with RM1021. **Are these true or are miss-assemblies??** 

* 05/06/2025
	* I selected Flye assembly genomes. I am trying to find a way to annotate variants. For example, in a CDS context. What variants are (non)synonymus? in which genes are? What mutations are point mutations/truncated protein? 
	* I found an extra plasmid. I will proceed with its identification, I will use MOB SUITES pipeline.