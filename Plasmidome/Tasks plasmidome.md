
- Describe assembled genomes
	- Genome sizes ✅
	- Genome coverage ✅
	- Number of contigs ✅
	- Similarity with reference (fastANI) ✅
	- Similarity using only chromosome (ezzaai) ⚠️

* Extract and cluster putative Plasmids:
	* Compute 3mer frequency (I saw 3mer produced the best balance between cluster variance-granularity) ✅ 
	* Extract cluster with more "Other" sequences ✅
	* Filter out < 10kb ✅
	* Establish Clusters with MobMess including PLSDB ⚠️
		* Using all the plasmids related to meliloti
		* Using all the plasmids related to meliloti < 500 kb

* Create ORFome:
	* Annotate Plasmids retrieved in the last step
	* Annotate PLSDB plasmids (including megaplasmids)
	* Cluster protein families (80% cov 50% id. ??? with UniRef50??)
	* 

* For each representative plasmid in a cluster:
	* Origin of replication prediction.
	* GC skew (maybe for those with no prediction? it depends on completeness tho)
	* Measure if similary Ori == similar plasmid (incompatibility group)

* For each cluster:
	* Number of genes overlapping between plasmid groups, and plasmids groups with pSymAB and chromosomes.

+ Describe plasmids
	- Presence of RepABC ✅
	- Presence of MOB. ✅
	- Presence of TA systems. ✅
	- Origin of Replication ✅
	- CDS ⚠️
	- Antismash (secondary metabolite biosynthetic) ⚠️
	- CAZymes ⚠️
	- AMPs ⚠️


* 
* intra and inter-species transfer events in plasmids groups, include database plasmids
* BGWAS underlying phenotype of having or not an accessory plasmid.
* pan-epiMethylation state clustering of plasmids


