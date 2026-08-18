# No RepABC

After MobMess de-replication and gene annotation, 374 out of 507 sequences presented a complete RepABC and 378 at least a RepA.

Some plasmids were below 44kb (the min to present a ), however they are ambiguous: contig_6_TG141 seems to be the same as contig_1_TG142 but miss-assembled with a duplication. These plasmids present RepF, lnc11 replicon group and MOBP,  predicted to be in Staphylococcus aureus (MOB-suite), but given their low occurrence and low coverage (<half or less than main replicons), they could represent contamination.

| Contig ID      | Product             | Copies | Length (bp) | GC %  |
| -------------- | ------------------- | ------ | ----------- | ----- |
| contig_1_TG142 | Replication protein | 1      | 8396        | 39.98 |
| contig_4_TG140 | Replication protein | 2      | 15817       | 40.95 |
| contig_6_TG141 | Replication protein | 2      | 19651       | 41.23 |

**RepB missing:** Cluster 281 composed of 3 large plasmids in dakota: *contig_5_TG190, contig_6_TG169 and contig_8_TG168*. They are victims of different gene annotation, maybe because of a divergent RepB. for example, one of them is annotated as Replication protein B but it does have the Gene symbo (repB), other member has the putative repB annotated as parB domain. all three members have a correct RepA and RepC annotation. Cluster 80 a singleton cluster: contig_4_TG71. It has the putative repB annotated as parB domain, and a correct RepA and RepC annotation. 

#  Curious Sequences

There is an example of what could be a complete novel plasmid. 
*contig_8_TG17* is a 15kb circular sequence not present anywhere else, it presents only a know two MOB (MOBV) and the rest are hypothetical proteins. Although, I suspect it is miss-assembled with a duplication. I estimate its size between 7-10kb. Check the [self-align dotplot](https://webfs/n/projects/jp2992/MOLNG4331/dakota_collab/flye_asm/TG17/medaka_polish/bakta_annot_TG17_asm/test_contig_8_TG17/output.png). Additionally, it has a coverage of 887x which is almost 8 times the chromosome (146x). Indeed, I found that the nearest sequence according to Mash distance (MOB-typer) is NC_004965, the smallest plasmid ever reported for *S. meliloti* by [Barran *et al.* (2001)](https://doi.org/10.1128/JB.183.8.2704-2708.2001)

*contig_8_TG153* is a 15kb sequence. MOB-typer found MOBP and predicted to be a multiphylla plasmids. the closest is a E. coli 3kb plasmid NC_019053 removed from the NCBI (idk why). it presents a coverage of 14x, the chromosome is 126x and less covered real large plasmid is 148x. This discrepancy in coverage make think it is contamination, plasmid loss or multi-strains. Interestingly, among annotations I find origin of replication, origin of transfer and ParB/ParA annotations. The [self-align dotplot](https://webfs/n/projects/jp2992/MOLNG4331/dakota_collab/flye_asm/TG153/medaka_polish/bakta_annot_TG153_asm/test_contig_8_TG153/output.png) does not indicate it is miss-assembled.

*contig_8_TG151* is a 3kb sequence, like in the previous case, MOB-typer predicted as multiphylla with NC_019053 as the closest. Gene annotation present a broad-spectrum class A beta-lactamase, a RNAI and a hypothetical protein (possible rep protein?). *contig_4_TG152* is the same plasmid but present a miss-assembly duplication. 
