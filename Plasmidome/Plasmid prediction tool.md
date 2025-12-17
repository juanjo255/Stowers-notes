
# About this

This is an extension of [[Plasmid prediction in illumina MAG strains]], but now focus on enhancing the strategy for accessory plasmid prediction in *Sinorhizobium meliloti.

The strategy will consist of prepare a pipeline including all the data learned in the past.

In summary, during the mentioned document we learned that the accessory plasmids and the mega-plasmids share giant amounts of DNA. Therefore, it is clear that the more fragmented a genome, the harder it will be to distinguish between an accessory plasmid and a mega-plasmid. 

Several tools with(out) Machine learning techniques were applied, but they were not good at all. It is clear that a mixed of them is needed and some of them are actually a mix ([[Plasmid prediction in illumina MAG strains]]). However, they were made to distinguish between chromosome and plasmid, and the assumptions in the difference between a chromosome and plasmid are higher than between a mega-plasmid and a acc. plasmid. 


RFPlasmid was the only tool I found trainable, and according to a recent [benchmarking](https://doi.org/10.1093/bib/bbaf589) between different plasmid prediction tools (RFPlasmid is integrated in PlasmidEC), RFPlasmid with Plasmer was among the best.

![[benchmarking_pls_tools.jpeg]]