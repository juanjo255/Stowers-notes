
Since it was difficult to update SMRT Link in the institute, I had to try to reproduce the steps that PacBio perform during the Microbial Genome Analysis which is not easy task they do not provide good documentation for this.

In this case I need to reproduce the steps to generate the following outputs documented in PacBio manual:

* **Motif Annotations**: GFF file listing every modified nucleotide annotated with the motif found by MotifMaker.
* **Modified Base Motifs**: CSV file containing statistics for the "methyltransferase" recognition motifs detected.


# TL;DR

After installation, you can use this script which contains all the steps `/n/projects/jp2992/MOLNG4331/biocomp_tools/custom_scripts/methyl_call_pacbio_hifi.sh`

See required files:
`methyl_call_pacbio_hifi.sh --help`


****

Let's start with the installation:


# Installation 

Once you get the installer from [PacBio web](https://www.pacb.com/support/software-downloads/),  The idea is to run this in command line so we only need to install the commands:

>`./smrtlink-release_25.3.0.273777_linux_x86-64_libc-2.17_anydistro.run --smrttools-only`

# STEP 1: cs-kinetics-bystrandify

Finding out this was the most horrible part, but I found the solution in this [issue](https://github.com/PacificBiosciences/kineticsTools/issues/95).

The problem is that during HiFi reads creation there is not **pi** and **pw** tags related with kinetics in SubRead Datasets, which is not the dataset that is form for HiFi reads, I do not really understand how the hell this work but it is in this way. So, these tags are missing and we have to first add them. So PacBio's solution was to add *pseudo* tags for compatibility:

> `ccs-kinetics-bystrandify unaligned.bam unaligned.kinetics.bam`

# STEP 2: pbmm2

After Step 1 we can align:

> `pbmm2 align --preset "HIFI" --sort H01_asm_flye.fasta MOLNG4331.H01_pseudoKineticTag.bam  > H01_aligned.bam `

Create indexes:

>```samtools index H01_aligned.bam
>pbindex H01_aligned.bam 
>```


# STEP 3: ipdSummary

Now, we can run methylation calling. This tool will give the modification in each base in the genome.

> ```
> pdSummary -j $cpus out.alignment.bam --reference reference.fasta --gff out.gff --csv out.csv --bigwig out.bigwig
> ```

# STEP 4: pbmotifmaker

Now, we can look for motifs. This program has two commands `find` and `reprocess` we must run both. The former will give the CSV with the motif and the latter will use the CSV produced by `find` to annotate the GFF we produce in the last step and which was the input of `find`

```
pbmotifmaker find -j $cpus B02_asm_flye.fasta B02_basemods.gff B02_motif.csv

```


```
pbmotifmaker reprocess -j $cpus B02_asm_flye.fasta B02_basemods.gff B02_motif.csv B02_basemods_w_motif.gff
```