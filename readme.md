# Mouse Brain - Single Cell Multiome ATAC + Gene Expression

## Overview

This repository demonstrates a workflow for the analysis of a multi-omics experiment interrogating chromatin accessibility and gene expression of the murine brain starting from raw fastq files all the way to downstream analysis. I use the Weighted Nearest Neighbour (WNN) method from the Seurat package to integrate expression and accessibility data for dimensionality reduction and finally cluster annotation. 

# Data

The data for this analysis is from 10x Genomics and can be found within their datasets archive under the name 'Fresh Embryonic E18 Mouse Brain (5k)'. This experimental data contains scRNA and scATAC-seq read outs from the same nucleus and was created using the 10x 'Epi Multiome ATAC + Gene Expression' protocol. The subject tissue is the brain of an 18 day old mouse embryo. We are therefore dealing with cells during differentiation that is likely becoming evident in the Multiomic data.

## Quality Control - raw data


# Workflow

0. Quality Control of all files

1. Indexing of reference genome

2. Align and create count/fragment table - cellranger

3. WNN Seurat Workflow

## preprocessing

Indexing of the genome

```{bash}
cellranger-arc mkref --config data/GRCm39_config.txt --nthreads=16 --memgb=22
```

## align and count

```{bash}
cellranger-arc count \
  --id e18_mouse_multiOmic \
  --reference data/GRCm39/ \
  --libraries data/raw_data/e18_mouse_brain_library.csv \
  --create-bam true \
  --localcores 16
```

## Quality Control - cellranger output








