# Mouse Brain - Single Cell Multiome ATAC + Gene Expression

## Overview

This repository demonstrates a workflow for the analysis of a multi-omics experiment interrogating chromatin accessibility and gene expression of the murine brain starting from raw fastq files all the way to downstream analysis. I use the Weighted Nearest Neighbour (WNN) method from the Seurat package to integrate expression and accessibility data for dimensionality reduction, cluster annotation, and finally the identification of features putatively interesting for cell type decisions.

This is intended as an exploratory analysis that serves only as a starting point for further analysis depending on the scientific question of the study.

The most important points are listed in this readme. The analysis is divided into 3 R-markdown files that contain the details and exact executed code.

## Data

The data for this analysis is from 10x Genomics and can be found within their datasets archive under the name 'Fresh Embryonic E18 Mouse Brain (5k)'. This experimental data contains scRNA and scATAC-seq read outs from the same nucleus and was created using the 10x 'Epi Multiome ATAC + Gene Expression' protocol. The subject tissue is the brain of an 18 day old mouse embryo. We are therefore dealing with embryonic cells during late gestation that are in varying stages of differentiation which is going to become evident in the analysis below.

## Quality Control - raw data


## Workflow overview

1. Align and create count/fragment table

2. Seurat WNN dim reduction

3. Cluster - Cell type association

4. Identify transcription factor Expression and Motif accessibility as cell tyoe markers

### indexing of the mouse reference genome

```{bash}
cellranger-arc mkref --config data/GRCm39_config.txt --nthreads=16 --memgb=22
```

### align and count

```{bash}
cellranger-arc count \
  --id e18_mouse_multiOmic \
  --reference data/GRCm39/ \
  --libraries data/raw_data/e18_mouse_brain_library.csv \
  --create-bam true \
  --localcores 16
```

### Quality Control - cellranger output

Unsurprisingly, the data deposited by 10x Genomics is of high quality. There is a clear association of scATAC-seq reads with Transcription Start Sites (TSS) of genes, and in most cell barcodes the fraction of reads mapping to peaks is over 0.5.

<div class="row">
  <div class="column">
    <img src="figures/QC/atac_TSS.png" alt="ATAC TSS" width="300"/>
  </div>
  <div class="column">
    <img src="figures/QC/atac_peaks_fragments.png" alt="ATAC fragment peaks" width="300"/>
  </div>
</div>

Similarly, the combined look at the RNA-seq and scATAC data shows most cells simultaneously having a high number of transposition events (ATAC) and a high number of UMIs (RNA).

![ATAC_GEX joint](figures/QC/joint.png)

## Dimensionality reduction and Clustering

Here, I am using Weighted Nearest Neighbor (WNN) to divide the cells into clusters. In this approach I rely on the individual dimensional reduction of the RNA and ATAC data to inform the decision.

How does this work?

What can we see?

![UMAP1](figures/umap.compare.RNA.ATAC.WNN.png)

## Cell type assignment

What did I use?

exemplary pictures of differentially expressed genes

## Transcription factor / Motif analysis

What did I do?

Show some interesting genes.
