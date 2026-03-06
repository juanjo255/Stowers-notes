
# Data

* Raw reads are located at [dakota_collab](https://webfs/n/projects/jp2992/MOLNG4331/dakota_collab/)

# Quality reads

These are Nanopore reads. Quality is not their strength. 

Here is a MultiQC report . 
There are additional NanoPlot plots in [raw_reads_QC](https://webfs/n/projects/jp2992/MOLNG4331/dakota_collab/P9/raw_reads_Nanoplot/) 

# Assemblies

For assembly I take two similar approaches:
1. My own pipeline.
2. Hybracter.

The reason for this is that due to the low coverage of these assemblies the psym and accesory plasmids get entagled



## To Note 
 
  I assembled using the pipeline Hybracter. It assemblies with Flye and includes Plassembler to get plasmids. A small comparison shows me that **Flye reported 54 samples** containing sequences below 500kb being circular, however **Plassembler recovered only in 18 of them**. One reason for this could be that Plassembler is actually sensible to coverage when using only long reads (maybe because of Unicycler? anyways its main purpose is to be used with hybrid assemblies). For example, 
<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/flye_asm_P9A10.png" height=300 > 
		
In the picture the helicopter propeller is probably the two psymA/B and there are apparently two circular acce. plasmids

<img src="https://webfs/n/projects/jp2992/stowers-notes/photos/plassembler_asm_P9A10.png" height=400 > 
		Plassembler in this case reported no circular plasmids. 