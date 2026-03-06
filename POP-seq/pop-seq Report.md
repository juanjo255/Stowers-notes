
# Tasks

For Amruthamshu:
1. Send BigWig coverage. ✅
2. Peaks in narrowPeak. ✅
3. Send the path to the reference motifs. ✅
4. To check in Amruthamshu output: G-quadruplex in motifs?


# Objective

We got data from POP-Seq (**P**rokaryotic chromatin **O**penness **P**rofiling **seq**uencing) for *Sinorhizobium meliloti* in two conditions: free living and bacteriods.

Here, Siva wants to check:
1. Differential peaks between bacteriods vs free living.
2. Find Motif differences between bacteriods and free living.

In the future, we can add RNA-seq data to POP-seq might give more hints. a TF can bind even if it is not expressed.


# Data 

> [!NOTE]
> Both conditions present a control which is a "naked" form of the genome that works to normalized noise background caused by the tn5.


Free living pop-seq data: 
> /n/projects/jp2992/sergio/pop_seq/pop_seq_free_living

Free living FASTQ
>/n/analysis/Sankari/sb2778/MOLNG-4289/3B0125D

L76151 and L76152 are the OnePercent_10min replicates and L76153 and L76154 are the control replicates

Bacteriods pop-seq data:
>/n/projects/jp2992/sergio/pop_seq/pop_seq_bacteriods

Bacteroid FASTQ
>/n/analysis/Sankari/sb2778/MOLNG-4543/3C0278L
L

80114_S2_L001 and 80115_S2_L001 are fixed and 80116_S2_L001 and 80117_S2_L001 are control


# Quality Check: Eukaryote vs Bacteria

The following plot is an example of a successful ATAC-seq in Eukaryotes. We can notice the peak around 200bp corresponding to nucleosomes and another one at 400bp, this is what is called refer as a "periodicity".

![[eukaryote_atacQC.png]]

For this bacteria, free living and bacteroid, the following plot would be consider a noisy ATAC-seq but in bacteria it represents the lack of size-fixed nucleosomes

![[bacteria_POPseq_QC.png]]



# Peak-calling 

Currently there are three approaches:

Genrich: it has an interesting approach for ATAc-seq using intervals centered on cut sites. I have not read about MACS BAMPE centering on the cutting sites. The disadvantage of this method is that is not published. Although the GitHub is well documented.

>Genrich command:
/n/projects/jp2992/sergio/pop_seq/peak_calling/code/peakcalling_genrich.sh

MACS2/3:This [source](https://nbis-workshop-epigenomics.readthedocs.io/en/latest/content/tutorials/ATACseq/lab-atacseq-bulk.html) mentioned that " MACS has more ATAC-seq oriented features than its predecessor MACS2, however, its main algorithm for peak detection is oriented towards peak calling in ChIP-seq experiments and does not take into account unique features of ATAC-seq data". However, other forums mentioned minimum differences, and compbio core has been using macs3.

>MACS3 command: /n/projects/jp2992/sergio/peak_calling/code/peakcalling_macs3.sh


HMMRATAC: This is not suitable for us, as it uses markov models for openness, nucleosome and background region. It is implemented as a subcommand in MACS3.



## Comparison: Genrich vs MACS3

The following IGV can show the differences between Genrich and MACS3

![[MACS3_vs_Genrich.png]]

For example, the Nod operon is not detected in MACS bacteroid.

![[NodOperon_MACsVsGenrich.png]]

Specifically in Genrich I wanted to compare the AUC value. I set 100 and 200. I added the MACS3 result as well:

| **File Name**                                                | **Number of Peaks** |
| ------------------------------------------------------------ | ------------------- |
| `bacteroid_200.narrowPeak`                                   | 1,631               |
| `bacteroid.narrowPeak`                                       | 2,085               |
| `freeLiving_200.narrowPeak`                                  | 4,600               |
| `freeLiving.narrowPeak`                                      | 5,084               |
| `macs3/merged_sorted_bacteroidsFixedvsCtrolPeaks.narrowPeak` | 658                 |
| `macs3/merged_sorted_freeLivingFixedvsCtrolPeaks.narrowPeak` | 1025                |

The point of the AUC is to find a balance between broad and narrow 
significant peaks. I continued with an AUC of 100.


Let's see how does it look like MACS3 vs Genrich vs CPM coverage through the whole Chromosome:

![[MACS3VsGenrichVsCoverage.png]]


I noticed what could be a bacteroids and free living transcription transition pointed by the move of the summit. Can this be an example of a transcription switch that can not be detected using MACS3??


![[transcriptRegul_switch_Genrich 1.png]]



# Differential Nucleoid Accessibility

> [!ATTENTION]
> **I used diffBind for both, but noticed that since Genrich return a consensus between replicates it changes parameters in DiffBind**
> 


## Genrich

The narrow peak file was used in *DiffBind* to perform differential peak calling. 
For this tools we must create a CSV sample sheet.

> Command: 
> /n/projects/jp2992/sergio/pop_seq/code/diffBind.R
> SampleSheet:
> /n/projects/jp2992/sergio/pop_seq/code/sample_sheet_diff_bind.csv


## MACS3

*MACS3* narrow peak file was used in *DiffBind* to perform differential peak calling. 

>Command: 
>/n/projects/jp2992/sergio/pop_seq/code/diffBind.R
>SampleSheet: 
>/n/projects/jp2992/sergio/pop_seq/code/sample_sheet_diff_bind.csv


### Results

/n/projects/jp2992/sergio/pop_seq/peak_calling/data/DB.sites.sorted.FullAnnot_w_headers.tsv: Contains the differential binding sites annotated with the last annotation Sergio suggested ([GCF_000006965.1/](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000006965.1/ "https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000006965.1/"))

The **DB.sites.sorted.FullAnnot_w_headers.pretty.tsv** version in the same folder presents the name of the chromosomes (e.g. pSymA)


### Plots

#### Consensus Peakset 

![[binding_sites_overlaps_all_venn.png]]


There are two methods to find differential peaks: DEseq2 and EdgeR.

#### DESeq2 vs EdgeR: Differential Binding Sites P-val < 0.05

![[deseq2_vs_edgeR.png]]


#### Differential Binding Sites: P-value < 0.05


![[bacteriods_vs_freeLiving_volcano.png]]

#### Gain and Loss Binding Sites: Bacteroids vs Free Living


![[bacteriods_gain_loss_binding_VennDiagram.png]]

#### tRNA exploration

During single-microbe RNA-seq we observed high number of tRNA expression in some cells. I wanted to check if this was observed here as well. And even if we seen an accessibility difference between both sample, some of them could be the consequence  of 16S RNA operon such as 

The plots of the 56 tRNA are at (normalized CPM):
>/n/projects/jp2992/sergio/pop_seq/peak_calling/data/tRNA_Profile_CPM.png




## Motif Calling

Using MEME-CHIP, First we can find motif enrichment in all peaks. This file it is needed by TOBIAS. Check:/n/projects/jp2992/sergio/pop_seq/motif_calling/code/motif_calling.sh

Some things to take into account:

1. I tested using background models using order 1 and 2. They perform similarly, and they are preferred than the order 0. So, I decided to continue with order 2 as it is the order used during *E. coli* database building and I want to avoid GC enrichment.
2. MEME needs us to indicate the number of motif we want to find. STREME does it automatically until p-value < 0.05.

**Output Folder:** /n/projects/jp2992/sergio/pop_seq/motif_calling

### Differential TF occupancy: highlighting motifs 

This was done with TOBIAS. Check:/n/projects/jp2992/sergio/pop_seq/motif_calling/code/motif_calling.sh

**Output Folder:** /n/projects/jp2992/sergio/pop_seq/motif_calling/data/TOBIAS

So, far we found no strong difference in TF ocuppancy predicitons between bacteroid and free living. Using scanning of 50 and 100 motifs.

#### Footprints comparison

Somethings I need to do before:

1. **Check the ATAC correction:** TOBIAS corrects the signal but I think it overshifted, one possibility is that POP-seq workflow handled this.
![[atac_correction.png]]
2. **Re-do peakcalling:** There is a confusion between using MACS3 or MACS2 with options `--nomodel --shift -100 --extsize 200 --broad` I am worried that because of the variability of sizes in bacteria data, **mostly might be either discarded or wrongly centered**.This suspicious comes from the weirdly flat footprint signal:
![[bound_footprint_comparison.png]]
3. 