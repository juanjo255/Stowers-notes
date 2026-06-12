# Objective

Find UppA-F cluster and podJ in *Bradyrhizobium* and *Sinorhizobium meliloti*

# Method

1. All sequences were downloaded using `datasets` command line tool from the NCBI
* For *Bradyrhizobium* references genomes were downloaded for each specie
	`datasets download genome taxon "Bradyrhizobium" --include gbff --assembly-source "RefSeq" --reference`
*  For *Sinorhizobium meliloti* genomes were downloaded using RefSeq to include strains 
	`datasets download genome taxon "Sinorhizobium meliloti" --include gbff --assembly-source "RefSeq"`
	
1. Sequences were searched using `Cblaster` 
	`/n/projects/jp2992/aleja/code/search_genes.sh`
	

# Result

## UppA-F

There’s a small challenge here when it comes to plotting the data. It turns out that the **UppC gene varies** quite a bit in terms of its distance from the other genes, and this **distance can be quite large** (>50 kb). 

Clustered heatmap: [https://webfs/n/projects/jp2992/aleja/bradyrhizobium_upp_genes_pretty_plot.html](https://webfs/n/projects/jp2992/aleja/bradyrhizobium_upp_genes_pretty_plot.html "https://webfs/n/projects/jp2992/aleja/bradyrhizobium_upp_genes_pretty_plot.html") 

Gene synteny: [https://webfs/n/projects/jp2992/aleja/upp_genes_synteny.html](https://webfs/n/projects/jp2992/aleja/upp_genes_synteny.html "https://webfs/n/projects/jp2992/aleja/upp_genes_synteny.html")

The synteny plot shows the top 100. As I mentioned earlier, you'll see that UppC appears last and that the reference genome is first.

**Extra files:**
1. **Binary:** shows the for each gene the presence/absence.
	`/n/projects/jp2992/aleja/cblaster_binary_brady_upp_genes_pretty.csv`
2. **Summary:** shows summary of the hist per gene per cluster.
	`/n/projects/jp2992/aleja/cblaster_summary_brady_upp_genes_pretty.csv`
  

## PodJ

  
**Clustered heatmap:** [https://webfs//n/projects/jp2992/aleja/bradyrhizobium_podj_genes_plot.html](https://webfs//n/projects/jp2992/aleja/bradyrhizobium_podj_genes_plot.html "https://webfs//n/projects/jp2992/aleja/bradyrhizobium_podj_genes_plot.html") 

**Gene synteny:** [https://webfs/n/projects/jp2992/aleja/podj_genes_synteny.html](https://webfs/n/projects/jp2992/aleja/podj_genes_synteny.html "https://webfs/n/projects/jp2992/aleja/podj_genes_synteny.html")

The synteny plot shows the top  50

**Extra files:**
1. **Binary:** shows the for each gene the presence/absence.
	`/n/projects/jp2992/aleja/cblaster_binary_brady_podj_genes.csv`
2. **Summary:** shows summary of the hist per gene per cluster.
	`/n/projects/jp2992/aleja/cblaster_summary_brady_podj_genes.csv
  