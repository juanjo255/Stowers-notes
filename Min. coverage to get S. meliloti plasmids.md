
# Antecedents

The idea is to know how low we can push coverage while getting complete circular plasmids.

Let's remember this benchmarking about plasmid recovery by Ryan Wick. 

<img 
src=https://webfs/n/projects/jp2992/stowers-notes/photos/plasmid_recovery_RWick.png />

**Notice** for our favorite assembly, Flye, the limit is around 10x. 

We can see this event in the collaborator data: 
<img height=400 src="https://webfs/n/projects/jp2992/MOLNG4331/collaborator_Smeliloti_hifi/flye_asm/stats_putative_pls/chromosomeCov_vs_accePlasmidCov.png"/> 
**Legend**: Number of chromosome assembled circular (mega-plasmids included).

**x-axis**: Mean Chromosome coverage (mega-plasmids included).

**y-axis**: Mean Coverage circular accessory plasmid.

The plot before show us that considering a median read length between 6-7kb and an uneven coverage between chromosome and plasmid we can get as low as 10x. Consider here that the minimum plasmid length recovered was 71,855 bp


# In-house test

Reads for all in-house strains were subsampled to 100x, 50x, 25x

<details>
<summary> Show code </summary>
```
fastq_files=(/n/analysis/Sankari/mm2883/MOLNG-4331/EA156900/LongPlex/longplex_output/MOLNG4331/merged_fastq/*.gz)

task_id=$SLURM_ARRAY_TASK_ID

file=${fastq_files[$task_id]}

fastqc_name=$(basename $file | cut -d "." -f 1,2 )

genome_size=7000000

median_read_len=$(grep -A 1000 '>>Sequence Length Distribution' /n/analysis/Sankari/mm2883/MOLNG-4331/EA156900/LongPlex/longplex_output/MOLNG4331/merged_fastq/QC/$fastqc_name"_fastqc/fastqc_data.txt" | sed '/^>>END_MODULE/q' | tail -n +3 | head -n -1 | sort -r -n -k2 | head -n1 | cut -f1 | cut -d "-" -f1)

target_coverages=(100 50 25)

for coverage in ${target_coverages[@]}

	do
	
	output_file=$(basename $file | cut -d "." -f 1,2)
	
	echo "#######"
	
	echo "Considering a median read length of:" $median_read_len
	
	echo "#######"
	
	num_reads=$(( $coverage * $genome_size / $median_read_len ))
	
	echo "For a coverage of $coverage'x' subsampling to this number of reads $num_reads"
	
	conda activate seqtk
	
	seqtk sample $file $num_reads > $(dirname $file)"/"$output_file"_"$coverage".fastq"

done
```
</details>


As expected, considering a median read length of 10-11kb, all the plasmids could be recover as low as 25x.

A02 is the only sample that could not achieve the expected assembly of 1 chromosome and 2 mega-plasmids, this is due to a repetition in the chromosome that make Flye to fragment it, however we have seen this being solve in other assemblers like Hifiasm.

A01, G01 and H01 were the only samples with more than 3 circular contigs which are the one that carry accessory plasmids, being A01 the one that carry 2 of them.


<img height= 400 src="https://webfs/n/projects/jp2992/stowers-notes/photos/subsampling_test_inhouse.png"/>