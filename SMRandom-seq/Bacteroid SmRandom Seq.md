# Antecedents

This is a Sergio's project. He wants to know if the results from scRNA-seq from M20 using SmRandom Seq are reliable.

For this Di previously prepared a matrix as well as processed the data with M20 pipeline.

It generates some clusters, but Sergio is concerned about it actually capturing the transcriptome differences in the nodule due to the low performance of this method <2000 cells. 

# Questions to answer

To prove this we will try to do: 

1. **Marker genes for Nodule zones.** Sergio mentioned there is a study that performed RNA-seq using microdissection of the nodule [laser_microDissection_RNA-seq](https://webfs/n/projects/jp2992/sergio/laser_microDissection_RNA-seq.pdf). From this paper we can get marker genes and see if several cells are presenting them. This could be a good signed of the technology capturing transcriptional differences. However this is not enough, it is easy to capture genes highly expressed, **what about the lowly expressed? Can the expression profile of each cluster be associated with any nodule zone?**  The L78684 dataset comes from bacteroids extracted from plants nodules. Each nodule contains 5 distinct zones where these bacteroids are hosted, and each of these zones contain bacteroids in different stages of differentiation. In one paper they did laser micro dissection coupled with RNA-seq on each of these zones (attached the paper just in case). I attached that data to this email as well. The idea here would be to find whether the clusters profiles found in L78684 are similar or not to any of the zones analyzed in that paper.

	> **Result:** This paper stablished clusters using also plants transcripts. You can noticed that in some clusters very few bacterial genes are apparently involved. However, there are some markers form different reports that were found differentially expressed on the different zone. Most of them were not found in our dataset, however I found some of them and they were involved in clustering, for example, KatA. 


2. **Correlation between free living and some cells in nodule**. if the technology is reproducible (consistency) then the free living transcription count must have a correlation with one of the clusters in the nodule as it is expected to have cells highly related to this stage in early stages of symbiosis .
	> **Result:** We performed integration of the dataset to see if we could see a clustering of free living. It was observed between SCT and Lognormalize, the latter being the better for this case. Sergio performed correlations between clusters as well, and found the same: A cluster closer to free living.


3. **Do the genes present in the same operons correlate in expression within each cluster?** To do so, there is a list of operons from a paper that predicts them _in silico_. I attached it to this email. I think that the data from L78684 should give more accurate information because its higher variability, but please correct me if I'm wrong.
	> **Result:** Sergio found consistency in the expression of important genes of symbiosis. These genes are found in the same operon so it was expected to see co-expression.

 

# Markers

| Gene ID  | Gene Name | Annotation Pattern | Published pattern Reference | % FI     | % FIId | % FIIp | % IZ     | % ZIII   |
| -------- | --------- | ------------------ | --------------------------- | -------- | ------ | ------ | -------- | -------- |
| SMa0869  | nodA      | ZI–ZII             | Sharma and Signor (1990)    | **62.2** | 7.5    | 1.8    | 2.6      | 25.9     |
| SMa0868  | nodB      | ZI–ZII             | Sharma and Signor (1990)    | **42.6** | 16.3   | 4.2    | 4.9      | 32.0     |
| SMa0866  | nodC      | ZI–ZII             | Sharma and Signor (1990)    | **35.1** | 23.8   | 9.2    | 8.8      | 23.2     |
| SMa1225  | fixK1     | IZ–ZIII            | Soupene et al. (1995)       | 1.5      | 0.6    | 2.3    | **28.3** | **67.2** |
| SMa0815  | nifA      | IZ–ZIII            | Sharma and Signor (1990)    | 2.4      | 0.5    | 0.4    | **27.5** | **69.2** |
| SMa1220  | fixN1     | IZ–ZIII            | Soupene et al. (1995)       | 1.1      | 0.5    | 3.7    | **25.6** | **69.1** |
| SMa0825  | nifH      | IZ–ZIII            | Labes et al. (1993)         | 0.9      | 0.3    | 0.2    | **31.1** | **67.5** |
| SMb20611 | dctA      | ZII–IZ–ZIII        | Boesten et al. (1998)       | 4.7      | 14.0   | 4.6    | **44.7** | **32.0** |
| SMc00819 | katA      | IZ–ZIII            | Jamet et al. (2003)         | 2.1      | 0.9    | 16.5   | **61.4** | 19.1     |
| SMb20007 | katC      | ZII and ZIV        | Jamet et al. (2003)         | 0.0      | 20.0   | 8.5    | 8.6      | **63.0** |
| SMa2379  | katB      | Non-specific       | Jamet et al. (2003)         | 23.6     | 25.0   | 19.6   | 18.5     | 13.3     |


| Cluster | %FI | %FIId | %FIIp | %IZ | %ZIII | M.t. | S.m  |
| ------- | --- | ----- | ----- | --- | ----- | ---- | ---- |
| 1       | 81  | 13    | 3     | 2   | 1     | 713  | 7    |
| 2       | 57  | 24    | 8     | 6   | 5     | 1338 | 83   |
| 4       | 41  | 33    | 13    | 5   | 7     | 1420 | 192  |
| 5       | 31  | 25    | 19    | 12  | 13    | 2269 | 849  |
| 3       | 16  | 48    | 22    | 7   | 7     | 735  | 250  |
| 11      | 13  | 17    | 29    | 28  | 14    | 1630 | 1336 |
| 10      | 1   | 5     | 61    | 28  | 4     | 441  | 18   |
| 9       | 1   | 1     | 10    | 68  | 20    | 1098 | 71   |
| 12      | 6   | 7     | 15    | 37  | 35    | 943  | 152  |
| 6       | 1   | 2     | 4     | 41  | 52    | 1039 | 111  |
| 7       | 3   | 3     | 3     | 12  | 79    | 427  | 490  |
| 8       | 10  | 11    | 11    | 15  | 53    | 353  | 892  |
| 13      | 15  | 15    | 16    | 21  | 33    | 1687 | 1026 |

A summary of cluster features (**mean of relative expression values in different nodule fractions for all genes of the considered cluster**), including the number of plant and bacterial genes in each cluster (right two columns);
clusters were ordered from maximum expression in FI (top, cluster 1) to
maximum expression in ZIII (cluster 7). The two bottom clusters (clusters 8
and 13) are substantially expressed in all nodule zones. Only genes showing
differential expression between at least two nodule fractions were considered.

Notice the clusters showed above were made considering genes in truncatula and meliloti.

# Some Thoughts

1. **tRNA real or fake:** There is a cluster interestingly made of tRNA. All the RNA come from this cluster. Which corresponds to around 1000 cells. As far as I know the rRNA is depleted using the CRISPR, but the tRNA is not. So, if tRNA is a problem of "contamination" in the sample, **shouldn't I see these distributed in multiple cells?** So this cluster is the one with the highest tRNA levels, however it is hard to say if this is an artifact:  

	> ![[Nodule_SCT_M20violin_seurat_clusters_percent.tRNA.png]]
	> 

2. **rRNA expression:** Siva is interested in observing if we can notice operon preference difference between the cells. Additionally, if we can see difference in rRNA expression levels. 

	> **Results:** for both free living and bacterios the rRNA-16s.2 was detected in most cells. however, it turns out that there are som reads carrying mutations that were uniquely mapped to one of the operons. But these operons are actually very similar, the one with more unique mappings is the one that can variate by some ncl. but it does not say anything. here the alignment:[rRNA16S_w_strand_clustalw.aln](https://webfs/n/projects/jp2992/sergio/map_reads/rRNA16S_w_strand_clustalw.aln) 


# Methods


## Clustering

Although the processing with Seurat has been quite easier than I was exprected in not completely trivial specially because depending on the dataset you might need a slightly different approach. The idea is to keep a biological logical story. I have learned a couple of things with this dataset:

1. **IntegrateData is different from IntegrateLayer.** This is the main reason I had so different results between LogNormalize and SCTransform and I thought that the problem was this normalization. But the problem is in summary that Integrate make a correction to the reductional space (PCA) of the whole dataset and IntegrateData does the correction on the counts creating a integrated assay (read this [issue](https://github.com/satijalab/seurat/issues/8653)) Using an integration like the CCA-based consist on finding anchors between variable features in each dataset so it reduces my dataset to a subset of common variable features 
2. **CCA-based integration may also lead to overcorrection between Free-living and Nodules hiding biological difference.** When I use this method that represent the default normalization method. I suspect it overcorrects the free-living data, as in nodule I have a lot less genes, and I end up with free-living being mixed with Nodule."CCA is well-suited for identifying anchors when cell types are conserved, but there are very substantial differences in gene expression across experiments."
3. **LogNormalize with Harmony differentiate between free-living and nodule, but it hides differences between nodule.** We know the nodule has different differential states and mix of states, so we should see these differences.
4. 