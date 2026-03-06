# Tasks 

1. Mine for more AMPs to build a model. There was not enough sequences. for most of them family model were found (PANTHER, Pfam). Tenecin_3 is the exception (check task 3) ✅
2. Build an HMM for each AMPs.✅
3. Run SPADA with CRP HMM model (Cystein rich).✅
4. Run SPADA with custom HMM model.
5. Assemble Transcriptome.✅
6. Look SPADA results in transcriptome.
7. Tenecin 3 has only around 3 reported genes. But it has a GGXXGG pattern I can look for in transcriptome. So I will try to build an HMM model (hoping that it takes the GGXXGG pattern) or I can try a regex approach.
8. Run AMPs prediction tools on T. molitor, fenugreek (NCR), sainfoin (NCR), plasmids.

# Objective

Dewey Leierer, Morgan Olmstead and Brenda Oppert at the university of Kansas are looking for AMPs peptides in the *Tenebrio molitor*.

The idea is to apply SPADA to look for more of these AMPs. The problem is that the amount of sequences are too small, so I have to try to mine for more similar to build a HMM model.

# Background

This is the information provided by Dewey:
  
1. Tenecin 1 (Q27023.1, 84 aa): Defensin family. Cysteine-rich, CSαβ motif with 3 disulfide bridges. Anti-Gram-positive. ([Moon et al., 1994](https://url.us.m.mimecastprotect.com/s/g7vnCER29rUlGGQ1cNfQI7RxFM?domain=academic.oup.com "https://url.us.m.mimecastprotect.com/s/g7vnCER29rUlGGQ1cNfQI7RxFM?domain=academic.oup.com"); [Kim et al., 1998](https://url.us.m.mimecastprotect.com/s/CepgCG625yUBllVWs7hJIB2uNI?domain=pubmed.ncbi.nlm.nih.gov/ "https://url.us.m.mimecastprotect.com/s/CepgCG625yUBllVWs7hJIB2uNI?domain=pubmed.ncbi.nlm.nih.gov/"))

2. Tenecin 3 (Q27270.1, 96 aa): Thaumatin-like protein family. Has conserved cysteine residues/disulfide bonds. Antifungal, constitutively expressed. ([Lee et al., 1996](https://url.us.m.mimecastprotect.com/s/s21yCJ62qGUBzz7pszivIyrdT_?domain=pubmed.ncbi.nlm.nih.gov/ "https://url.us.m.mimecastprotect.com/s/s21yCJ62qGUBzz7pszivIyrdT_?domain=pubmed.ncbi.nlm.nih.gov/"))

3. Tenecin 4 (BAL04117.1, 143 aa): Attacin family. Glycine-rich (~14% Gly), ~120 aa mature form. Anti-Gram-negative, bactericidal against E. coli. ([Chae et al., 2012](https://url.us.m.mimecastprotect.com/s/T3yECKr2ZKtDwwj8hAsRI5tUqi?domain=pubmed.ncbi.nlm.nih.gov/ "https://url.us.m.mimecastprotect.com/s/T3yECKr2ZKtDwwj8hAsRI5tUqi?domain=pubmed.ncbi.nlm.nih.gov/"))

4. Coleoptericins A, B, and C (AII26031.1, AII26032.1, AII26033.1; 119, 127, and 118 aa): Glycine-rich (>20% Gly), no cysteines. Anti-Gram-negative. These represent what was originally characterized as "Tenecin 2" ([Roh et al., 2009](https://url.us.m.mimecastprotect.com/s/YYgACL928MtkOOJNTjt7IytmX3?domain=europepmc.org "https://url.us.m.mimecastprotect.com/s/YYgACL928MtkOOJNTjt7IytmX3?domain=europepmc.org")) and was subsequently resolved into three distinct genes ([Zhu et al., 2014](https://url.us.m.mimecastprotect.com/s/no9vCM82QOS288QxI1u6I8VgLw?domain=sciencedirect.com "https://url.us.m.mimecastprotect.com/s/no9vCM82QOS288QxI1u6I8VgLw?domain=sciencedirect.com")). There is no separate Tenecin 2 deposited in NCBI.

So apparently these are validated AMPs. I need to either produce HMM model or find one for the family that I can be used in SPADA for mining.

1. Tenecin 1 (Q27023.1, 84 aa): It presents a PANTHER HMM model [DEFENSIN (PTHR13645)](https://www.pantherdb.org/panther/family.do?clsAccession=PTHR13645) built with 11 genes. Check the [PDB entry for more](https://www.uniprot.org/uniprotkb/Q27023/entry#family_and_domains)
2. Tenecin 3 (Q27270.1, 96 aa): it does not present HMM model, but there are 3 sequences clustered at 50%. It should be a start to create a HMM model: [cluster](https://www.uniprot.org/uniref/UniRef50_Q27270) . Additionally, it has a strong GGXXGG pattern that can be searched. 
3. Tenecin 4 (BAL04117.1, 143 aa): There is not HMM model, nor cluster of similar proteins. However there is a HMM model for the predicted family in Pfam what corresponds to [Attacin, C-terminal region](https://www.ebi.ac.uk/interpro/entry/pfam/PF03769/logo/) 
4.  Coleoptericins A, B, and C (AII26031.1, AII26032.1, AII26033.1; 119, 127, and 118 aa): There is not HMM model, nor cluster of similar proteins. However there is a Pfam model for [Coleoptericin](https://www.ebi.ac.uk/interpro/entry/pfam/PF06286/logo/)



# Using SPADA

SPADA by default uses Augustus and GeneWise for gene prediction. It includes other methods but the authors found that this combination provides the higher sensitivity.The code only allows to select the gene model of 3 plant genomes. So, I had to modified the code to look for the **tribolium** model for the gene prediction of *T. molitor*


## Predict CRP with SPADA

The CRP models can help us find Cystein rich genes. SPADA only found 6 genes that presented a signal peptide.However, without the signal peptide signal filter, It found around 1627 genes 

>Cys-rich Genes with signal peptide
>/n/projects/jp2992/MOLNG4331/biocomp_tools/spada/SPADA_GCF_963966145_tribolium/61_final.tbl


> Cys-rich Genes no signal peptide
>/n/projects/jp2992/MOLNG4331/biocomp_tools/spada/SPADA_GCF_963966145_tribolium_no_filter/61_final.tbl



# Assemble Transcriptome

I found RNA reads collected from the *T. molitor* body. Reads were filtered with *FastP* and assembled using *RNASPAdes*. Additionally, super-transcripts were assembled following *Salmon+Corset+Lace*. Finally, transcriptome completeness was assessed with *BUSCO* using *polyphaga_odb12* dataset. 

>Assembly script
>/n/projects/jp2992/AMPs_predict_T_molitor/code/transcriptome_asm.sh

> Transcriptome folder
> /n/projects/jp2992/AMPs_predict_T_molitor/assemblies/rnaspades_fastp


**BUSCO Completeness** returned a high value of 95% completeness. It looks like a decent transcriptome to look for the AMPs.

![[busco_completeness.png]]

```markdown
***** Results: *****

C:95.0%[S:18.6%,D:76.4%],F:3.0%,M:2.0%,n:4010      
3810    Complete BUSCOs (C)                        
745     Complete and single-copy BUSCOs (S)        
3065    Complete and duplicated BUSCOs (D)         
120     Fragmented BUSCOs (F)                      
80      Missing BUSCOs (M)                         
4010    Total BUSCO groups searched
```

>[!Curious]
>Something curious is that during super transcript, the duplication dropped to 6% but the Completeness as well down to 89% 
>/n/projects/jp2992/AMPs_predict_T_molitor/assemblies/rnaspades_fastp/BUSCO_Lace 


# tBLASTn on transcriptome

The AMPs validated in *T. molitor* sent by Dewey were queried against the transcriptome 6-translated using tBLASTn.



# PSI-BLAST on transcriptome

ORFs from transcriptome were extracted using orfipy and The AMPs validated in T. molitor sent by Dewey were queried using PSI-BLAST, to retrieved similar sequences.