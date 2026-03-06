# Data Description

* In total 119 *S. meliloti* strains were assembled and shared by a collaborator of Siva. 

* Genomes are stored in [collaborator_Smeliloti_hifi](https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/)

[multiqc_report.htm](https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/raw_reads/QC/multiqc_report.html) Quality report of the PacBio reads.

We can noticed that compared to Siva's PacBio they counted with less number of reads and a smallest median read length. Given that Siva's sequencing has 10 times more data than the collaborator, I subsample to 20k reads to achieve similar amount of data as the collaborator. At the end, Siva's counted with a mean read length between 14522 -15000 bp per sample, whereas the collaborator presents median between 6249-7249 bp.

On the other hand, the authors of the data tried to keep coverage around 50x. In the plot below, we can find a mean of the mean coverage per contig in each assembly. 

![[description_stats_penn_state.png]]

We can see minimum coverages down to 10x, therefore, it was very common to find ambiguous assemblies between accessory plasmids as well as between accessory plasmids and the symbiotic plasmids (pSym), especially pSymA.




# Genome assembly

[descriptive_stats_collaborator_genomes_pacbio.ipynb](https://webfs/n/projects/jp2992/MOLNG4331/code/descriptive_stats_collaborator_genomes_pacbio.ipynb): contains descriptive plots of assemblies.

# Completeness

Only **m64404e_240531_162148.hifi_reads.bc2090--bc2090** could not achieve *Ensifer* marker genes in CheckM. So It was removed.




