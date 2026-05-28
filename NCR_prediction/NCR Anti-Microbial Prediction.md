# Tasks

1. Run AMP prediction to the 3000 (bukh.. dataset) NCRs ✅
2. Run AMP prediction on fenugreek NCRs ✅
3. Run AMP prediction on sainfoin NCRs ✅
4. In AMPSeek check if there are differences between full and mature. I am afraid that the mature limit the colabfold prediction ⚠️

# Table of Content

```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
include: 
exclude: 
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```


# Methods

I will use the following tools for anti-Microbial activity prediction:

1. **APEX**: A deep learning model trained on two sources. The primary in-house dataset contained 988 peptides with 14,738 MIC measurements across 34 bacterial strains, heavily weighted toward human gut and clinical pathogens. This was augmented with publicly available data from DBAASP: 5,093 AMPs and 5,500 non-AMPs, where non-AMP was defined as MIC > 30 μmol/L. The peptide sequences were encoded using the AAindex, a 566-dimensional vector of physicochemical and biochemical properties per amino acid. **The in-house peptides are predominantly from human and animal sources and only two plant species appear in the entire extinctome dataset**
	![[APEX_wf.png|300]]
2. **AMPseek**: Complete pipeline that predicts antimicrobial activity (*AMPlify*), tertiary structure (*LocalColabFold*), and toxicity (*tAMPer*). **tAMPer was trained using ESM2 embeddings!!** 

	 ![[AMPSeek_workflow.png|300]]
	
3. **pyAMPA**: Predict AMP regions in proteins. it predicts MIC against some bacterial models as well as *Cell-penetrating*, *AMPValidate*, *Hemolytic* and *Toxic* probabilities. **For NCRs, it worked interestingly**. NCR247 showed highest Cell-penetrating prob.
	![[pyAMPA_workflow.png | 300]]

# Results

> [!ATTENTION]
> **All prediction were performed on the mature peptides** to reduced false positive AMP activity possibly coming from the signal peptide.
> 

In our case APEX performed poorly. pyAMPA presents better results were *NCR247* showed highest Cell-penetrating probability, which it is a feature Siva suspects about this NCR. AMPSeek...



## Boukherissa dataset
 
**FASTA**: `/n/projects/jp2992/NCR_screening/Boukherissa_full_fixed_mature.fasta`

| type    | num_seqs | sum_len | min_len | avg_len | max_len |
| :------ | :------- | :------ | :------ | :------ | :------ |
| Protein | 3,710    | 155,931 | 13      | 42      | 169     |
### APEX
In our case this model perform poorly.
Output: `/n/projects/jp2992/NCR_screening/apex_antimicrobial_prediction/Predicted_MICs_Boukherissa_v2.csv`

### pyAMPA
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction/pyampa_out/results_boukh.xlsx`

### AMPSeek
Here I predicted on full and mature to compared
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction`

## Fenugreek
**FASTA**: `/n/projects/jp2992/NCR_screening/fenugreek/mature_pep/61_final_noDups.mature.checked.fasta`

| type    | num_seqs | sum_len | min_len | avg_len | max_len |
| :------ | :------- | :------ | :------ | :------ | :------ |
| Protein | 823      | 54,540  | 22      | 66.3    | 200     |

### APEX
In our case this model perform poorly.
Output: `/n/projects/jp2992/NCR_screening/apex_antimicrobial_prediction/Predicted_MICs_fenugreek_v2.csv`
### pyAMPA
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction/pyampa_out/results_fenugreek.xlsx`

### AMPSeek
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction`


## Sainfoin
**FASTA:** `/n/projects/jp2992/NCR_screening/sainfoin/mature_pep/61_final_noDups.mature.checked.fasta`


| type    | num_seqs | sum_len | min_len | avg_len | max_len |
| :------ | :------- | :------ | :------ | :------ | :------ |
| Protein | 1,173    | 106,640 | 20      | 90.9    | 199     |


### APEX
In our case this model perform poorly.
Output: `/n/projects/jp2992/NCR_screening/apex_antimicrobial_prediction/ Predicted_MICs_sainfoin_v2.csv`

### pyAMPA
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction/pyampa_out/results_sainfoin.xlsx`

### AMPSeek
Output: `/n/projects/jp2992/NCR_screening/AMP_prediction`


