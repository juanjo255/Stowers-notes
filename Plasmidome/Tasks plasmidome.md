# Symbol Glossary
⚠️ To Do but I postponed it
✅ Done
✅⚠️ Done but must be reviewed




# To Do
- Describe assembled genomes
	- Genome sizes ✅
	- Genome coverage ✅
	- Number of contigs ✅
	- Similarity with Rhizobiaceae (fastANI) ✅
	- Similarity using proteome against reference (ezzaai) ✅

* Establish strains populations with popPunk. 

* **Extract and cluster putative Plasmids:**
	* Compute 3mer frequency (I saw 3mer produced the best balance between cluster variance-granularity) ✅ 
	* Extract cluster with more "Other" sequences ✅
	* Filter out < 10kb ✅
	* Establish Clusters with MobMess including PLSDB ✅
		* Using all the plasmids related to meliloti ✅
	* Create folder for each backbone, compound and maximal cluster. ✅

* **Plasmid cluster descriptions:**
	* Number of unique plasmids ✅
	* Number of sequences per dataset ✅
	* Presence of MOB ✅ 
	* Presence of RepABC ✅ 

* * **Establish Rh groups according to**: https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000351 ✅

* **For each representative plasmid in a cluster:**
	* Origin of replication prediction. ✅
	* GC skew (maybe for those with no prediction? it depends on completeness tho) ⚠️


 * **Create ORFome:**
	* Annotate Plasmids retrieved in the last step ✅
	* Annotate PLSDB plasmids (including megaplasmids) ✅
	* Cluster protein families (panaroo/PPanGGoLin) ✅
	* Plot PCA with protein families per plasmid ✅
	* Assign GOCs to plasmids and plot in PCA.✅
	* Plot PCA with GOCs.✅
	* Annotate defenses system with defense finder. Any defense enriched in accessory plasmids?
		* annotate in chromosome
		* annotate in psymA
		* annotate in psymB
		* annotate in acc. pls
	* Map IS in pan-genome.
	* Create single-version of networks with LIONESS. This might help us visualize how the samples interactions differ when plasmids are removed. In this case I do not have phenotypic outcomes, so everything would be just function-based. 


* For each cluster:
	* Number of genes overlapping between plasmid groups, and plasmids groups with pSymAB and chromosomes.

+ Describe plasmids
	- Presence of TA systems. ✅
	- CDS 
	- Antismash (secondary metabolite biosynthetic) 
	- CAZymes 
	- AMPs 




distribution of pSyms, chromosome and accessory plasmid per isolation

* intra and inter-species transfer events in plasmids groups, include database plasmids
* BGWAS underlying phenotype of having or not an accessory plasmid. (?)
* pan-epiMethylation state clustering of plasmids

1. I could use https://github.com/liampshaw/rmsFinder to look for type II R-M system and predict target. ✅