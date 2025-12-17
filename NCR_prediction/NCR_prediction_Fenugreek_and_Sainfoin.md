
# Background

Siva collaborated in an interesting [paper](https://doi.org/10.1101/2025.09.09.675119) that looked for establish the phylogenetic relationships of NCR Legumes.

**They used all the publicly Legumes genomes as well as the RNA-seq data** from the plants below:

| Clade         | Species                 |
| ------------- | ----------------------- |
| IRLC          | Medicago truncatula     |
|               | Medicago sativa         |
|               | Pisum sativium          |
|               | Cicer arietinum         |
|               | Trifolium pratense      |
|               | Melilotus officinalis   |
| Dalbergioids  | Arachis hypogaea        |
|               | Aeschynomene evenia     |
| Robinoids     | Lotus japonicus         |
| Genistoids    | Lupinus albus           |
|               | Lupinus luteus          |
|               | Lupinus mariae-josephae |
| Milletioids   | Cajanus cajan           |
|               | Phaseolus vulgaris      |
|               | Vigna angularis         |
|               | Glycine max             |
| Indigoferoids | Indigofera argentea     |

# Objective

**Predict NCR peptides on fenugreek and Sainfoin**. 
	Because both genomes are not available in the NCBI, they were not predicted during Siva's collaboration. Fenugreek does not have a genome and Sainfoin does, however it is not published in the NCBI yet (as by 10-nov-2025).


# Data

The Sainfoin genome was retrieved from its [paper](https://doi.org/10.1038/s42003-023-05754-6) (as of 17-nov-2025 it is not in the NCBI)

The Fenugreek genome was assembled with Spades with the DNA data generated in this [paper](https://doi.org/10.1016/j.fochms.2021.100044) and saved under the SRA code [ERR5639085](https://trace.ncbi.nlm.nih.gov/Traces?run=ERR5639085) 

The Fenugreek transcriptome was assembled with RNA_Spades using the following public data: SRR14721915, SRR14721912, SRR14721913, SRR14721911, SRR14721914, SRR14721916



# Methods


## Classical

The plan was to apply [SPADA](https://github.com/orionzhou/SPADA) a pipeline to predict NCRs.The pipeline is very old, therefore it was very difficult to install and run.

Here, for future learning I present the two approaches taken:
1. [ncr_prediction_pre_spada](https://webfs/n/projects/jp2992/stowers-notes/photos/ncr_prediction_pre-spada.png)
2. [ncr_prediction_w_spada](https://webfs/n/projects/jp2992/stowers-notes/photos/ncr_pred_w_spada.png) (This is the good method)

The workflows are for editing in [Miro](https://miro.com/app/board/uXjVJaFw9G8=/?focusWidget=3458764635583399063)

**TL;DR:** The SPADA output was filtered by length (200aa) and number of Cysteine of mature peptides (>=4Cys). An the matured peptide classified using the HMM models for IRLC and Dalbergioids generated in this [paper](https://doi.org/10.1101/2025.09.09.675119).

To validate the methods, Medicago truncatula was annotated and the curated list ([ref_mtruncatula_NCRs.csv](https://webfs/n/projects/jp2992/NCR_screening/ref_truncatula/NCR_screening/ref_mtruncatula_NCRs.csv) of NCR (715 NCRs) from M. truncatula taken from [Morphotype of bacteroids in different legumes correlates with the number and type of symbiotic NCR peptides](https://www.pnas.org/doi/pdf/10.1073/pnas.1704217114) used to confirm the results using MMseqs2 as aligner.


> [!QUESTION]
> Siva asked: Is it possible to predict anything with a signal? Yes, but the false positive are high. I have seen than just getting ORFs. Thousands get signal peptide. 
> 

****

### Results

The following results are from SPADA:

All the metrics are for the filtered peptides.

| Species                   | Number of NCRs | Number of NCRs (filtered) | sum_len | min_len | avg_len | max_len | Homology annotation file                                                                                                                   |
| ------------------------- | -------------- | ------------------------- | ------- | ------- | ------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| M. Truncatula             | 1,205          | 940                       | 89,214  | 42      | 94.9    | 227     | [CRPs_w_cluster_w_seq.tsv](https://webfs/n/projects/jp2992/NCR_screening/truncatula/SPADA_truncatula/CRPs_w_cluster_w_seq.tsv)             |
| Sainfoin                  | 1,804          | 1,173                     | 135,010 | 39      | 115.1   | 225     | [CRPs_w_cluster_w_seq.tsv](https://webfs/n/projects/jp2992/NCR_screening/sainfoin/SPADA_sainfoin/CRPs_w_cluster_w_seq.tsv)                 |
| Fenugreek (transcriptome) | 626            | NAN                       | 58,234  | 23      | 93      | 622     | [CRPs_w_cluster_w_seq.tsv](https://webfs/n/projects/jp2992/NCR_screening/fenugreek/SPADA_fenugreek_transcriptome/CRPs_w_cluster_w_seq.tsv) |
| Fenugreek (genome)        | 609            | NAN                       | 51,579  | 21      | 84.7    | 353     | [CRPs_w_cluster_w_seq.tsv](https://webfs/n/projects/jp2992/NCR_screening/fenugreek/SPADA_fenugreek_genome/CRPs_w_cluster_w_seq.tsv)        |
| Fenugreek all (no dups)   | 1,083          | 823                       | 74,090  | 47      | 90      | 243     | [CRPs_w_cluster_w_seq.tsv](https://webfs/n/projects/jp2992/NCR_screening/fenugreek/SPADA_fenugreek_all/CRPs_w_cluster_w_seq.tsv)           |


The following results were for the alternative workflow (just for learn):

RBH=Reciprocal Best Hit

| Species                   | Number of NCRs | RBH to M. truncatula Curated List |
| ------------------------- | -------------- | --------------------------------- |
| Medicago Truncatula       | 992            | 466                               |
| Sainfoin                  | 1614           | 56                                |
| Fenugreek (transcriptome) | 427            | 169                               |

As you noticed the number of retrieved peptides was lower than the expected. Particularly, in M. truncatula NCR247 was not found. Fortunately, Jonathon was abled to fix the SPADA pipeline and I could learnt why I was not finding NCR 247 in my predictions: SPADA reported that a mix of different gene predictors cause differences in sensitivity. The best sensitivity was provided by the default: Augustus Evidence; GeneWise & SplicePredictor. **It turned out that the sensitivity was compromised because I was using only Augustus_Evidence and NCR247 was found by GeneWise;SplicePredictor!**



## Curious fact

I tried to confirmed the NCRs using the proteome. Only 13 NCRs were detected (cov. and id. 0.9 ). Confirming that even 12 year after SPADA pipeline, current annotators are still not ready to annotate CRPs.

****

## ESM

In this case, I am gonna try the ESM model which is a protein language models that predict protein structure. It can be trained on NCR peptides to see how good it is at predicting peptides. 

Jay tried this before and organized a code that it will make my life easier. the code is here: `/n/core/bigDataAI/Sankari_lab/ssankari/20250324_ncr_esm_model`

I move copy the code in this directory: `/n/projects/jp2992/NCR_screening/code/20250324_ncr_esm_model`

### Positive and Negative datasets


For ESM training, I must provide two with my positive result and my negative, so the model does not "get lazy" focusing on the evident features of the NCRs which are the Cysteines. 

**The positive dataset** is composed of the "curated" list of NCRs in each plant. I start first with A. Thaliana, and the NCRs dataset from Boukherissa. 

**The negative dataset** is composed of all the ORFs-Cysteines rich found in the 6-frame translated genome that also presented a signal peptide according to SignalP4. Minus the Curated dataset.

**Remove the curated from the positive** consisted of getting the nucleotide form of the negative dataset and map the curated using Miniprot. The use of Miniprot is because it is fast and we have to consider the existence of the introns in the ORFs. The alternative is to make a simple BLASTP search and get the best matches.
	1. Translate Genomes
	2. Extract ORFs: Here, **ORF is everything before a stop codon** it does not matter if it does not have a start codon. This is to make sure we have all the exons. 
	3. Get Cys rich and ORFs.
	4. Map known NCR to genome with Miniprot.
	5. Extract Gene of known NCR. 
	6. Translate 5 in 6-frames as in 2 and keep only Cys-rich ORFs.
	7. Remove Cys-rich ORFs generated at 6 from 3
	8. Train positive on curated (or on 6) and negative on 7.

The idea is to make predictions on 3, however it has a problem. The amount of data. For Thaliana it was plausible because after strep 3 I got 95kb sequences, and it did not take much time for ESM (around 40 min), but for truncatula that is not the case. I got aprox. 300k sequences! (I am waiting for it to finish to see time)


Therefore, I came to a new idea that arose during my chitchatting with Eric. I can reduce much more the dataset if I look for the signal peptide. To do this I might need to concat the ORFs as they were split by the STOP codon. These are the steps I will take:

1. For each ORF search upstream (+) or downstream (-).
2. Select the a 1000 pb with the gene centered and look for signalp5 on complete ORFs.
3. Remove nested.

Alternative that might be better:
1. Slide the genome in 2kb windows.
2. Translate windows into 6-frames.
3. Keep regions with Cys-rich and signal pep.






### Predictions

I made three trainings:
1. Boukherissa full seq.
2. Boukherissa mature seq.
3. Thaliana mature. 

The idea is to predict on 6-translated ORFs. So, there are cases where I will have the peptide in either one exon with the signal peptide or split in two exons. where I can recognize the mature peptide. The signal pep can lead to false positive as we could see before. Getting Cys-rich ORFs and Signal peptide, I get thousands of results.