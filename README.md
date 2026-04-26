# 10x-Genomics-Spatial-Transcriptomics-Methods-
The repository covers spatial transcriptomics using Scanpy and Squidpy across four tutorials. It analyzes 10x Genomics Visium (H&amp;E &amp; fluorescence) and Xenium data, covering QC, clustering, image feature extraction, spatial statistics, and tissue visualization.

# Notebook 1: Basic Scanpy Spatial Analysis

This notebook demonstrates a basic **spatial transcriptomics workflow** in **Scanpy**. It first analyzes a **10x Visium human lymph node** dataset and then applies a similar workflow to a second dataset with manually added spatial coordinates.

---

## Requirements

Main Python packages used:
- `scanpy`
- `anndata`
- `pandas`
- `matplotlib`
- `seaborn`

---

## File

- `Basic Scanpy.ipynb`

## Overview

The analysis includes:
- loading spatial transcriptomics data
- computing quality-control metrics
- filtering low-quality spots and genes
- normalizing and log-transforming counts
- selecting highly variable genes
- running PCA, neighbors, UMAP, and Leiden clustering
- visualizing clusters and gene expression in tissue space
- identifying marker genes

---

## 1. Import libraries

The notebook imports the main Python libraries needed for:
- plotting with `matplotlib` and `seaborn`
- data handling with `pandas`
- spatial transcriptomics analysis with `scanpy`

## 2. Set Scanpy options

Scanpy settings are configured to:
- print package versions for reproducibility
- set figure size and style
- enable detailed logging output

## 3. Load Visium dataset and compute QC metrics

A built-in **10x Visium human lymph node** dataset is loaded with Scanpy.  
Mitochondrial genes are identified, and quality-control metrics are calculated for each spatial spot.

## 4. View the AnnData object

The dataset is stored in an `AnnData` object, which contains:
- the gene expression matrix
- observation metadata
- variable metadata
- spatial coordinates
- image information

## 5. Plot QC histograms

Histograms are used to inspect:
- total counts per spot
- number of genes detected per spot

These plots help choose appropriate filtering thresholds.

## 6. Filter spots and genes

Low-quality spots and rarely detected genes are removed based on:
- minimum total counts
- maximum total counts
- mitochondrial percentage
- minimum number of spots per gene
- 
## 7. Normalize and find highly variable genes

The data is:
- normalized to make spots comparable
- log-transformed to stabilize variance
- reduced to highly variable genes for downstream analysis

## 8. Dimensionality reduction and clustering

The notebook performs:
- PCA for dimensionality reduction
- nearest-neighbor graph construction
- UMAP for visualization
- Leiden clustering to identify groups of similar spots

## 9. Plot UMAP

UMAP plots show the distribution of spots in low-dimensional space and allow comparison between:
- QC features
- cluster assignments

## 10. Plot QC features in tissue space

QC-related features such as total counts and detected genes are visualized directly on the tissue image to identify spatial quality patterns.

## 11. Plot clusters in tissue space

Cluster labels are overlaid on the tissue image to show how transcriptionally defined groups are arranged spatially.

## 12. Zoom in on selected clusters

Specific clusters are highlighted in a cropped tissue region to examine local spatial organization in more detail.

## 13. Find marker genes for clusters

Differential expression analysis is used to identify genes that are enriched in specific clusters.

## 14. Plot a marker gene in space

A selected marker gene is visualized together with cluster labels to help interpret the biological identity of clusters.

## 15. Plot additional genes in space

Additional genes are plotted in tissue space to compare their spatial expression patterns across the sample.

## 16. Import AnnData directly

The `anndata` package is imported so a second spatial dataset can be created manually.

## 17. Load coordinates and count matrix

The second dataset is assembled from:
- a coordinate file
- a count matrix file

This creates a new `AnnData` object for analysis.

## 18. Match coordinates with expression data

Only observations present in both the coordinate table and count matrix are kept, and their spatial coordinates are added to the dataset.


## 19. Process the second dataset

The same standard workflow is applied to the second dataset:
- normalization
- log transformation
- PCA
- neighbors
- UMAP
- Leiden clustering

## 20. Plot clusters for the second dataset

The final results for the second dataset are visualized in:
- UMAP space
- spatial coordinate space

---

## References

[Scanpy spatial tutorial](https://scanpy-tutorials.readthedocs.io/en/latest/spatial/basic-analysis.html)

[Squidpy Visium fluorescence tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_fluo.html)

[Squidpy Visium H&E tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_hne.html)

[Squidpy Xenium tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_xenium.html)

[10x Genomics Xenium Human Lung Cancer Dataset](https://www.10xgenomics.com/datasets/xenium-ffpe-human-lung-cancer)
