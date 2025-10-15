
This [issue](https://github.com/PacificBiosciences/kineticsTools/issues/95) pointed the solution to a problem I was having when running `ipdSummary` 

The problem was that ipdSummary was not detecting pi and pw tags related with kinetics, however this applies to SubRead not for HiFi, so these tags are missing and we have to first add them (pseudo):

> `ccs-kinetics-bystrandify unaligned.bam unaligned.kinetics.bam`


Now we can align:

> `pbmm2 align --preset "HIFI" --sort H01_asm_flye.fasta MOLNG4331.H01_pseudoKineticTag.bam  > H01_aligned.bam `

Create indexes and run modification calling:

>```samtools index H01_aligned.bam
>pbindex H01_aligned.bam 
>pdSummary -j 20 out.alignment.bam --reference reference.fasta --gff out.gff --csv out.csv --bigwig out.bigwig```
