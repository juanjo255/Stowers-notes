

# Antecedents 

[Sneideris et al. (2023)](https://doi.org/10.1038/s41467-023-42374-4) used a machine learning model to predict phase propensity. *"The machine learning analysis reveals that a substantial fraction of AMPs are predicted to phase separate either alone (i.e. homotypic phase separation) or in the presence of nucleic acids"*


Interestingly, [Yang et al. (2025)](https://doi.org/10.1093/bib/bbaf393) create a framework to use protein-protein interaction (PPI) networks and the protein sequence to predict Liquid-Liquid phase separation (LLPS). The follow image shows their benchmarking. 


![[LLPS_benchmark.jpg]]


# Tasks

1. Run DeepPhase.
2. Run FruzDrop

# Data

**Boukherissa NCRs:** `/n/projects/jp2992/NCR_screening/Boukherissa_full.fasta`

# DeePhase

DeePhase was run using its [GitHub Repo](https://github.com/kadiliissaar/DeePhase). It was slightly modify to run on every NCRs from the boukerissa dataset. **Code:** `/n/projects/jp2992/MOLNG4331/biocomp_tools/DeePhase` 

**Output:** `/n/projects/jp2992/NCR_screening/deePhase_results`


# FuzDrop

FuzDrop depends on the disorder values from ESpritz which although it is free, it is not open source. I had to asked for it. However, it did not work, I think FuzDrop code is broken. 

So I had to use the [FuzDrop](https://fuzdrop.bio.unipd.it/predictor). Since, it accepts only one protein per request. I created a python script using `Curl` to make automatic requests. **Code:** `/n/projects/jp2992/MOLNG4331/biocomp_tools/fuzdrop_api_request`

**Output:** `/n/projects/jp2992/NCR_screening/fuzdrop_results`






