Here I sum up some of the interesting papers I have read to guide my paper construction.

# To Read ⚠️

[The complete replicons of 16 _Ensifer meliloti_ strains offer insights into intra- and inter-replicon gene transfer, transposon-associated loci, and repeat elements](https://doi.org/10.1111/mec.16704) this is what I am doing

[Transposon-plasmid nesting enables fast response to fluctuating environments](https://doi.org/10.1101/2025.06.04.657954) This study investigates the prevalence of transposons in plasmids relative to chromosomes. Authors *hypothesized that this nested structure provides unique adaptive advantages by combining transposition-driven genetic mobility with plasmid-mediated copy number amplification*.

[Genome-wide systematic identification of methyltransferase recognition and modification patterns]( https://doi.org/10.1038/s41467-019-11179-9) demonstrate a high-throughput method for *coupling methyltransferases with their respective motif*

# Read ✅
1. [plasmid classification](https://doi.org/10.1016/j.plasmid.2023.102684): review of the plasmid classification methods. They agree with what I was suspecting. "*In clustering approaches used for plasmid classification, thresholding is highly dataset dependent. [...] .What is needed is to provide content to such species for them to be meaningful, and not simply another way of naming plasmid groups.Just as a single bacterial species contains a variety of strains that can differ by many traits, plasmid species could exhibit intra-species variation in any part of their backbones as a reflection of different adaptations"*
2. [RepA and RepB exert plasmid incompatibility repressing the transcription of the repABC operon](https://doi.org/10.1016/j.plasmid.2013.08.001): evaluate the similarities and differences between the molecular mechanisms underlying the transcriptional regulation of the p42d repABC operon and other Type Ia par operons, including parAB from P1 plasmids and sopAB from F plasmids. We also describe the crucial role that the transcriptional repression of the repABC operon plays in plasmid incompatibility.

3. [plasX and MobMess](https://doi.org/10.1038/s41564-024-01610-3) MobMess is the tool I will use to decontaminate and cluster my plasmids. I like its strategy to handle fragmentation cases. **It can help me establish clusters resistant to plasmid fragmentation.**
4. [Pathways for horizontal gene transfer in bacteria revealed by a global map of their plasmids](https://doi.org/10.1038/s41467-020-17278-2) This is the COPLA. The first global network of plasmids and establishment of PTUs. Total of 276 PTUs in the bacterial domain. Each PTU exhibits a characteristic host distribution, organized into a six-grade scale (I–VI), ranging from plasmids restricted to a single host species (grade I) to plasmids able to colonize species from different phyla
5. [Phage-plasmids promote recombination and emergence of phages and plasmids](https://doi.org/10.1038/s41467-024-45757-3) They studied the gene flow between phages, phages-plasmids and plasmids. in previous studies they established an interesting metric to measure the similarity between MGEs called wGRR (weighed Gene Repertoire Relatedness) and **it can help me to track HGT events**.
6. [A widespread group of large plasmids in methanotrophic _Methanoperedens_ archaea](https://doi.org/10.1038/s41467-022-34588-9): Description of two new plasmids (~150kb) for methane archaea. 
	1. They described large plasmids, limited to a specific specie of archaea and with low information available. Additionally, Borgs are thought to expand metabolic capacity, check next paper.
	2. they are like a chromid, where the plasmid acquire some host's DNA, however they decided to called them **Borgs**, maybe cuz it does not imply a dependance on them, however one of the plasmids carried tRNA missing in the host, so they inferred dependance. 
	3. One of the plasmids encoded for a nucleoid protein MC1, interesting... 
7. [Borgs are giant genetic elements with potential to expand metabolic capacity](https://doi.org/10.1038/s41586-022-05256-1) 
		*"We can neither prove that they are archaeal viruses or plasmids or minichromosomes, nor prove that they are not. Although they may ultimately be classified as megaplasmids, they are clearly different from anything that has been previously reported."* Borgs presents low GC, no plasmids replication-conjugation system, no viral proteins. As I see it, they are like megaplasmids but chromosome related. they harbor metabolic related genes and they are thought to augment methane oxidation (not tested yet).
8. [Non-conjugative plasmids limit their mobility to persist in nature](https://doi.org/10.1016/j.celrep.2025.116456) 
	* This is very interesting because might be related to the question of why *S. meliloti* has so many large plasmids. Most of its plasmids are greater than 100kb.
	* It explains interesting concepts such as the ways plasmids can mobilize:
		1. **Conjugative plasmids**: They are self-transmissible. They harbor all the machinery and tend to be large. related with antibiotics.
		2. **Non-conjugative**: They need to hijack a conjugative machinery of other plasmid or use alternative methods such as phage/phage-inducible chromosomal island (PICI)-mediated, transformation or membrane vesicles. 
		3. **Non-transmissible**: These are a subtype of non-conjugative. but they do not have any mechanism to hijack others conjugation machinery. They rely exclusively on the alternative methods.
	* Using *S. aureus* authors found that non-conjugative plasmids does not present proteins related to phage-mediated transduction. Although they can easily develop phage-mediated mobility (they induced phage acquisition through evolution experiment), *"low plasmid transfer enables plasmids to co-exist and protect host bacteria and neighbors from threats. However, increased movement reduces plasmid diversity, eroding protective benefits and leaving populations vulnerable."*
	* I find the tested hypothesis from the authors super interesting, because it reminds me of a thought I had time ago about these plasmids representing complex compositions of *S. meliloti* subpopulations, where some could present beneficial phenotypes for the whole population. In this study the authors found that plasmid low mobility allows enhancement of community diversity. When there is hyper-mobility of plasmids causing one type plasmid dominance, it produces detrimental to the population by reducing its capacity to respond to enviromental stress. Interestingly, this was observed in their last experiment, where using 2 different plasmids harboring two different protections, indicated that an *"optimum population survival occurred when the two plasmids were present at a 50:50 ratio and was compromised if either plasmid was dominant"* (familiar???)
	* This cool illustration summarizes de hypothesis:
		![[low_mobility_pls_theory.jpg]]
9. [What makes a megaplasmid?](https://doi.org/10.1098/rstb.2020.0472) Review trying to answer what makes a megaplamid and why they are megaplasmid. This cool picture resume the paper:
		![[What_makes_megaplasmid.png]]
10. [Toxin-Antitoxin Systems Reflect Community Interactions Through Horizontal Gene Transfer](https://doi.org/10.1093/molbev/msae206) Interesting study found that HGT communities have unique and predictable TA signatures. They built a random forest using the frequency of TA systems and achieved 95% accuracy of PTUs prediction. **They found that the frequency of TA systems decreases as plasmid length increases, supporting the idea that acquiring more TA systems reach a saturation point where it does not give more benefit and this can be alleviated by gaining other accessory genes**.
11. [Plasmid transmission dynamics and evolution of partner quality in a natural population of Rhizobium leguminosarum](https://doi.org/10.1128/mbio.02497-25)  They investigated the diversity of plasmids in *R. leguminosarum*. I like their way to cluster the plasmids, it is what I was looking for. A clustering core gene-based where I can cluster more on a function-based. Some things interesting:
 > 	 I found something similar with pSymB (i have not confirmed the reliability of mine tho): *"Interestingly, four of the 62 strains lacked the pSym (as previously found based on short-read assembled genomes), further corroborating that this non-essential element could be lost in strains present within a naturally occurring population"* 
 > 	The use of GRF metric to compared phylogenetic trees between chromosome and plasmids is also interesting for our purpose. It is interesting (and I still do not know if I like it) to determine if a plasmid were moving vertically or horizontally. 
 > 	Based on the ratio of shared polymorphisms to fixed differences between 12 Sinorhizobium medicae and 32 S. meliloti strains, few HGT events (97 genes out of 3986 genes examined) were observed [49](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000351#R49). **Nearly all of the HGT events involved plasmid-localized genes**.

12. [Mobility of Plasmids](https://doi.org/10.1128/mmbr.00020-10)  discussed the mobility in plasmids. how plasmid conjugation, and together with accessory genes, they have evolved into specific systems adapted to specific physiological and ecological contexts.

13. [Ecological dynamics and complex interactions of _Agrobacterium_ megaplasmids](https://doi.org/10.3389/fpls.2014.00635) 
14. **Can Phages drive specialization?** (this was a presentation in the symbiosis conference, Canada).  phage drive tradeoff in symbiotic traits. experimental evolution of R. leguminosorum with 3 different phages. similarly, when in nodule they are more susceptible to phage infection. 


| ![[IMG_3744.jpeg\|200]] | ![[IMG_3745.jpeg \| 200]] |
| ----------------------- | ------------------------- |





