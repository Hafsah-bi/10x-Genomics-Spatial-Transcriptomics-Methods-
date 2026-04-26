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

# Notebook 2: Analyze Visium Fluorescence Data

This notebook demonstrates how to analyze **10x Genomics Visium fluorescence data** using **Squidpy**.  
The workflow includes loading spatial transcriptomics data, visualizing clusters and fluorescence channels, segmenting nuclei, extracting image-derived features, and comparing image-based clustering with gene-expression-based clustering.

---

## Overview

The analysis follows this workflow:

1. Import packages and load the dataset  
2. Plot spatial clusters  
3. Show fluorescence channels  
4. Smooth and segment the image  
5. Extract segmentation features  
6. Extract multi-scale image features  
7. Define feature clustering function  
8. Cluster spots by image features  

---

## Dataset

This example uses a **preprocessed crop** of a **mouse brain Visium fluorescence dataset** provided through Squidpy datasets.

- `img`: fluorescence image stored as a Squidpy `ImageContainer`
- `adata`: spatial transcriptomics data stored as an `AnnData` object

The fluorescence image includes multiple channels used for downstream visualization and segmentation.

---

## Requirements

Install the main dependencies before running the notebook:

- squidpy
- scanpy
- anndata
- pandas
- matplotlib

---

## 1. Import packages and load data

This step imports the required libraries and loads the image and AnnData objects used throughout the notebook.

## 2. Plot spatial clusters

This plot shows the annotated transcriptomic clusters in their spatial tissue coordinates.

## 3. Show fluorescence channels

This visualization displays the individual fluorescence channels separately.

## 4. Smooth and segment the image

The image is first smoothed to reduce noise, then watershed segmentation is applied on channel 0.  
A cropped region is displayed to compare the raw image and segmentation result.

## 5. Extract segmentation features

Segmentation-based features are computed for each spot using the segmented image.  
These features can then be compared with gene-expression-based clusters.

## 6. Extract multi-scale image features

This step computes summary, histogram, and texture features at different scales and contexts, then combines them into one feature table.

## 7. Define feature clustering function

A helper function is defined to cluster selected image features using scaling, PCA, neighborhood graph construction, and Leiden clustering.

## 8. Cluster spots by image features

This final step clusters spots separately using summary, histogram, and texture features, and compares the resulting image-based clusters with the original transcriptomic clusters.

---

# Notebook 3: Analyze Visium H&E Data

This notebook shows how to analyze **10x Genomics Visium H&E spatial transcriptomics data** with **Squidpy** by combining spatial gene expression, tissue image features, neighborhood analysis, ligand-receptor analysis, and spatial autocorrelation.

---

## Overview

The workflow in this notebook includes:

1. Import packages and load data  
2. Plot spatial clusters  
3. Extract summary image features at multiple scales  
4. Cluster spots using image features  
5. Build the spatial neighbor graph and test neighborhood enrichment  
6. Analyze cluster co-occurrence  
7. Perform ligand-receptor interaction analysis  
8. Compute spatial autocorrelation of genes  
9. View top Moran’s I results  
10. Plot spatially variable genes  

---

## Dataset

This example uses a **preprocessed Visium H&E mouse brain dataset** provided through Squidpy.

- `img`: H&E tissue image stored as a Squidpy `ImageContainer`
- `adata`: spatial transcriptomics dataset stored as an `AnnData` object

The dataset includes pre-annotated clusters and associated histology image data.

---

## Requirements

Install the main dependencies before running the notebook:

- squidpy
- scanpy
- anndata
- numpy
- pandas

---

## 1. Import packages and load data

This step imports the required libraries and loads the H&E image and the preprocessed spatial transcriptomics dataset.

## 2. Plot spatial clusters

This plot shows the annotated gene-expression clusters in their spatial tissue coordinates.

## 3. Extract summary image features at multiple scales

This step computes summary image features for each spot at multiple scales to capture both local and broader tissue context.  
The extracted feature tables are then combined into a single matrix for downstream analysis.

## 4. Cluster spots using image features

A helper function is used to cluster spots based on the extracted image features using scaling, PCA, neighbor graph construction, and Leiden clustering.  
The resulting image-based clusters are compared with gene-expression-based clusters.

## 5. Build the spatial neighbor graph and test neighborhood enrichment

This step constructs the spatial connectivity graph between spots and tests whether certain clusters are located near each other more often than expected.

## 6. Analyze cluster co-occurrence

This analysis measures how frequently one cluster appears near another across spatial distances, helping reveal spatial organization patterns between tissue regions.

## 7. Perform ligand-receptor interaction analysis

This step identifies potential cell-cell communication signals between clusters using ligand-receptor expression analysis and highlights interactions between selected source and target groups.

## 8. Compute spatial autocorrelation of genes

This analysis calculates Moran’s I for highly variable genes to identify genes with spatially structured expression patterns.

## 9. View top Moran’s I results

This step displays the top-ranked genes based on Moran’s I statistics.

## 10. Plot spatially variable genes

This plot visualizes selected spatially variable genes together with the cluster map to compare expression patterns across tissue regions.

---

## References

[Scanpy spatial tutorial](https://scanpy-tutorials.readthedocs.io/en/latest/spatial/basic-analysis.html)

[Squidpy Visium fluorescence tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_fluo.html)

[Squidpy Visium H&E tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_hne.html)

[Squidpy Xenium tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_xenium.html)

[10x Genomics Xenium Human Lung Cancer Dataset](https://www.10xgenomics.com/datasets/xenium-ffpe-human-lung-cancer)
