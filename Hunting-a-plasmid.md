# Objective 1: Is it Real?

An extra putative plasmid was identified. The task is to figure out if it is a plasmid or a sequencing artifact or error.

## Where was it found?
***
The plasmid was identified in sample H01 (MAG215). During whole genome assembly a short sequence was assembled by Hifiasm and Flye. Their length differ significantly, and only Flye was abled to identify this sequence as circular (table and pictures below).

Flye was thought for small to medium genomes and has been characterized for been very good at circularizing bacterial genomes and plasmids, while Hifiasm was thought for generate haplotype-resolved assembly of big genomes (created for human genome). Hifiasm has in-heritage the string graph strategy its author has been developed since Miniasm and which tended to produce longer/duplicated sequences. Therefore, in this case, given the similarity between both plasmids assembled, I prefer continue with Flye's plasmid assembly.

| Assembler | len (bp) | circular |
|:---------:|:--------:|----------|
|   Flye    | 192,654  | Yes      |
|  Hifiasm  | 240,319  | No       |

## Plasmid assembly features
***
Now, I described the observations that supports the presence of this plasmid. Let's start with coverage.

### Coverage
The extra plasmid presented a coverage congruent with the rest of the genome. In the next table we can see all the sequences assembled by Flye, just by looking at the length we can tell which are the main chromosome, the 2 classic plasmids and the extra plasmid (contig_4).

| ID       | Len       | Cov |
| -------- | --------- | --- |
| contig_1 | 1,689,003 | 551 |
| contig_2 | 3,654,821 | 558 |
| contig_3 | 1,328,226 | 630 |
| contig_4 | 192,654   | 772 |

Plasmids can be identified looking for:
1. Relaxases proteins.
2. Mating Pair Formation system (MPF).
3. OriT.
4. Replication Initiation Protein (RIP).
5. OriV. 

***MOB Suites*** was used for typing the putative plasmid for numeral **1, 2 and 3**. It was abled to found relaxase proteins. Additionally, they were from a different type regarding to the other two big plasmids usually found in *S. meliloti*. The tool could not find MPF and OriT, reason why it is expected to be a mobilizable plasmid, but not conjugate (table below). Additionally, it returned the accession of the plasmid on their database with which the putative plasmid shares higher number of k-mers and it turns out to be an accessory plasmid reported in *S. meliloti* strain HM006. 

Finally, as expected, it was not found any relaxase, OriT or MPF in the main chromosome. 

| ID       | len     | relaxase_type | relaxase_type_accession(s) | mash_nearest_neighbor | mash_neighbor_identification |
| -------- | ------- | ------------- | -------------------------- | --------------------- | ---------------------------- |
| Contig_4 | 192,654 | MOBP          | CP026529_00118             | CP021832              | Sinorhizobium meliloti       |

**See complete result here:** [H01_mobtyper_results.tsv](https://webfs/n/projects/jp2992/MOLNG4331/flye/H01/new_plasmid/H01_mobtyper_results.tsv )

***OriV-Finder*** was used to annotate the putative plasmid for numeral **4 and 5**. The tool was able to predict an OriV based on the finding of RIPs of type RepA and RepC (figure 1 and figure 2). 

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/oriV.png" class="wikilink"
alt="oriV.png" />
<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/oriV_iterons.png" class="wikilink"
alt="oriV_iterons.png.png"/>
**Figure 1.** OriV prediction close to a GC skew and a RIP (top). Prediction is supported by AT rich region and prediction of putative Iteron (bottom). |
| <img src="https://webfs/n/projects/jp2992/stowers-notes/photos/repA_new_plasmid.png" class="wikilink"
alt="repA_new_plasmid.png"/>
<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/repC_prediction_new_plasmid.png" class="wikilink"
alt="repC_prediction_new_plasmid.png"/>
**Figure 2.** RIPs found in putative plasmid (contig_4). |

# Objective 2: Is it known? 

During [Objective 1](https://webfs/n/projects/jp2992/stowers-notes/Hunting-a-plasmid.html#objective-1-is-it-real) the existence of the plasmid was confirmed. The task is to determine similarity to other accessory plasmids reported in *S. meliloti*, in order to find homology and function clues.

For ease, from now on I will refer to the plasmid found in MAG215 as **pMAG215**.

## pMAG215 a novel plasmid in *S. meliloti* 
***
According with Siva and Madi there are a couple of accessory plasmid reported, and some of the most described are **pSmeSM11a, pRmeGR4b and pTA2** (I could not find the last one in the database).

Therefore, we need to know if the plasmid was reported before and if not where we can find homology that gives clues about its functions.

Around 753 sequences related with the keywords *Sinorhizobium meliloti\[All Fields\] AND plasmid\[filter\]* were downloaded from the NCBI. Sequences were filtered for greater than **10kb** and lower than **500kb** to remove the two big plasmids, the chromosome and genes or cassettes. The final dataset contained **114** sequences. **No similar was found among 75 sequences mapped**, only short regions of probably homology (Figure 3). **This might indicate is a new plasmid**. The sequences compiled contained also the plasmids the indicated by Siva: pSmeSM11a, pRmeGR4b.

[Dataset with 114 sequences](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/plasmids_smeliloti_filtered.fasta)

However, the plasmid showed some degree of homology to other plasmids reported in Sinorhizobium that might help figuring out functions associated in other studies. In the pMAG215 annotation section we will see an example of stretches related to other plasmids in Sinorhizobium, in that case specifically to *S. medicae*.

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/plasmids_vs_new_plasmid_asm5.png" class="wikilink"
alt="plasmids_vs_new_plasmid_asm5.png"/>
**Figure 3.** Alignment of 75 plasmids reported for S. meliloti in the NCBI to plasmid found in MAG215 (contig_4).

Mapping the new plasmid to PLSDB, a plasmid database by the NCBI, confirmed previous results (Figure 4).
<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/PLSDB.png" class="wikilink"
alt="PLSDB.png"/>
**Figure 4.** Results returned by PLSDB using new plasmid (contig_4) as query. This database contains more plasmids than the ones we used since it includes different species. 

## pMAG215 annotation
***
### BAKTA
Annotation of the extra plasmid with BAKTA **shows a 34% of hypothetical proteins**. Figure 5 shows genome map with predicted CDS and ncRNA and table below shows descriptive stats of annotation.

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/plot-feat.png" class="wikilink"
alt="plot-feat.png"/>
**Figure 5**. Genome mapping summarizes CDS prediction. First ring forward. Second ring

**pMAG215 annotation statistics**

| Genome | GC   | Coding ratio | ncRNA | ncRNA region | CDS | CDS hypothetical | CDS pseudogene |
| ------ | ---- | ------------ | ----- | ------------ | --- | ---------------- | -------------- |
| H01    | 58.9 | 78.5         | 1     | 1            | 241 | 82               | 5              |

### PGAP

The annotation was updated using the NCBI pipeline PGAP. It showed a significant reduction in annotation. **From now on, we will keep using this annotation**. This will work as a comparison for future.

**pMAG215 annotation statistics**

| Genome | GC   | Coding ratio | CDS | CDS hypothetical | CDS pseudogene |
| ------ | ---- | ------------ | --- | ---------------- | -------------- |
| H01    | 58.9 | 77           | 217 | 54               | 42             |


Using the pMAG215 annotation, once again, we confirm the nature of this contig as a plasmid. Figure 6 is showing the replication module ***RepABC*** reported in other plasmids of *S. meliloti* such as ***pSmeSM11b***, additionally we see homology in this region with the plasmids aligned previously, supporting the annotation of these proteins. This was done with BAKTA, but same results were found in PAGP annotation

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/RIPs_all_plasmids_vs_pmag215.png" class="wikilink"
alt="RIPs_all_plasmids_vs_pmag215.png"/>
**Figure 6.** Region in pMAG215 predicted for RepABC showing homology to other plasmids in Sinorhizobium.


### Gene Ontology clustering

***
This is an example. KEGG was abled to annotate only 21%. 51 out of 241.

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/keeg_annot.png" class="wikilink"
alt="keeg_annot.png"/>


# Objective 3: Homology in pMAG215

During [Objective 2](https://webfs/n/projects/jp2992/stowers-notes/Hunting-a-plasmid.html#objective-2-is-it-known) We aligned pMAG215 with 114 accessory plasmids downloaded from NCBI and found that pMAG215 had not been reported before as no similar plasmid existed. However, we found that the pMAG215 overlapped in some regions with 75 plasmids suggesting regions of homology.

## KH35c
***
Siva found some similarities between genes of interest in pMAG215 and the accessory plasmids of KH35c (pKH35cA). Strain KH35c is important as Siva has observed <span style="color:#079e15;font-style: italic">some similar plant phenotype between KH35c and MAG215</span>.

During the mapping to the 114 accessory plasmids of *S. meliloti*, pKH35cA was included and actually was among the best matches. **The next table presents the 10 best matches**.

* [plasmids_vs_new_plasmid_blast.tsv](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/plasmids_vs_new_plasmid_blast.tsv) Presents details about all the accessory plasmids in *S. meliloti* with significant matches to pMAG215 using BLAST.

* [plasmids_vs_new_plasmid_blast.out](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/plasmids_vs_new_plasmid_blast.out) Presents all the plasmids with significant matches to pMAG215 and their pairwise alignments.

* [igv_session.xml](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/igv_session.xml) This is an IGV session where you can visualize all the significant matches to pMAG215 with gene annotation of pMAG215. I presents to type of alignment: one up to 20% of divergence with Minimap2, and second with local alignment with BLAST.

| Accession  | Description                                                                  | Score | E-value |
| ---------- | ---------------------------------------------------------------------------- | ----- | ------- |
| CP140898.1 | Sinorhizobium medicae strain ml49 plasmid pMl1, complete sequence            | 21529 | 0.0     |
| CP140966.1 | Sinorhizobium medicae strain ml20 plasmid pMl1, complete sequence            | 21461 | 0.0     |
| CP021832.1 | Sinorhizobium meliloti strain HM006 plasmid accessoryA, complete sequence    | 17385 | 0.0     |
| CP003934.2 | Sinorhizobium meliloti GR4 plasmid pRmeGR4a, complete sequence               | 13372 | 0.0     |
| CP021826.1 | Sinorhizobium meliloti strain KH35c plasmid accessoryA, complete sequence    | 13372 | 0.0     |
| CP178489.1 | Sinorhizobium meliloti strain RPZ17 plasmid pSkuRPZ17-1, complete sequence   | 13104 | 0.0     |
| JQ665880.1 | Sinorhizobium meliloti plasmid pHRC017, complete sequence                    | 12050 | 0.0     |
| CP088116.1 | Sinorhizobium meliloti strain RRI128 plasmid pRRI128_3, complete sequence    | 11867 | 0.0     |
| CP140912.1 | Sinorhizobium medicae strain ml29 plasmid pMl5, complete sequence            | 10750 | 0.0     |
| CP021796.1 | Sinorhizobium meliloti strain USDA1157 plasmid accessoryA, complete sequence | 10744 | 0.0     |

### Protein to protein alignment
***Roary*** with **80% of identity** was used to clustered similar proteins between pKH35cA and pMAG215. The next table presents gene shared between them.

* [gene_presence_absence.xlsx](https://webfs/n/projects/jp2992/MOLNG4331/extra_plasmid_H01/aln_homologous/kh35c/roary_result_80_pct_1751036011/gene_presence_absence.xlsx) Contains all the genes clustered between pKH35cA and pMAG215.

