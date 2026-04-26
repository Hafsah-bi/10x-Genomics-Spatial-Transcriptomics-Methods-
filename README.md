# 10x-Genomics-Spatial-Transcriptomics-Methods
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

![QC Histograms](https://github.com/Hafsah-bi/10x-Genomics-Spatial-Transcriptomics-Methods-/blob/main/results/Basic%20Scanpy%20Spatial%20Analysis/1.%20qc_histograms.png)
> *Figure 1. Histograms of total counts and detected genes per spot/cell used for initial quality control assessment. Full-range and zoomed-in views are shown to highlight the overall distribution and potential filtering thresholds.*

**Key observations**
- Total counts are centered around **~20,000 UMIs** for most observations.
- Detected genes are concentrated around **~5,000–6,000 genes**.
- Low-count and low-gene outliers are present, consistent with potential low-quality spots/cells.
- The distributions are moderately right-skewed, with a subset of high-count observations.
- These plots provide a basis for selecting **QC filtering cutoffs** prior to downstream analysis.

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

![UMAP plots](results/Basic%20Scanpy%20Spatial%20Analysis/2.%20umap%20plots.png)
> *Figure 2. UMAP embedding colored by total counts, detected genes, and cluster identity to assess quality control trends and transcriptional heterogeneity across the dataset.*

**Key observations**
- The embedding shows **multiple distinct clusters** with clear separation in UMAP space.
- Total counts and detected genes display **broad gradients** across the embedding.
- Regions with higher total counts generally also show **higher gene complexity**.
- The clustering identifies **10 transcriptionally distinct groups**.
- The overall structure suggests **biological heterogeneity** rather than purely technical variation.

## 10. Plot QC features in tissue space

QC-related features such as total counts and detected genes are visualized directly on the tissue image to identify spatial quality patterns.

![Spatial counts](results/Basic%20Scanpy%20Spatial%20Analysis/3.%20spatial%20counts.png)
> *Figure 3. Spatial maps of total counts and detected genes overlaid on the tissue image, illustrating how sequencing depth and transcript complexity vary across the section.*

**Key observations**
- Total counts and detected genes exhibit **clear spatial heterogeneity** across the tissue.
- Areas with higher counts generally show **higher gene complexity**.
- A central low-signal region is visible in both panels.
- The shared spatial pattern suggests that **UMI abundance and detected genes are strongly correlated**.
- These plots help identify **regions that may require QC consideration** before downstream analysis.


## 11. Plot clusters in tissue space

Cluster labels are overlaid on the tissue image to show how transcriptionally defined groups are arranged spatially.

![Spatial clusters](results/Basic%20Scanpy%20Spatial%20Analysis/4.%20spatial_clusters.png)
> *Figure 4. Spatial map of Leiden cluster assignments overlaid on the tissue image, showing the organization of transcriptionally distinct regions across the section.*

**Key observations**
- Clusters 0–9 show **clear spatial heterogeneity** across the tissue.
- Several clusters form **coherent regional domains**.
- Some cluster boundaries appear sharp, while others are **more intermixed**.
- The observed pattern suggests **structured tissue organization** with potential biological regionalization.
- These results support downstream **cluster annotation and marker identification**.

## 12. Zoom in on selected clusters

Specific clusters are highlighted in a cropped tissue region to examine local spatial organization in more detail.

![Spatial clusters zoom](results/Basic%20Scanpy%20Spatial%20Analysis/5.%20spatial_clusters_zoom.png)
> *Figure 5. Zoomed-in spatial map showing selected cluster assignments and background spots within a local tissue region.*

**Key observations**
- Clusters **5** and **9** show **localized spatial structure**.
- Cluster 5 is more broadly represented, while cluster 9 appears in **smaller discrete patches**.
- **NA** spots are concentrated near non-tissue or excluded regions.
- The panel highlights **fine-scale heterogeneity** within the tissue.
- This view helps assess **local cluster organization** in histological context.

## 13. Find marker genes for clusters

Differential expression analysis is used to identify genes that are enriched in specific clusters.

![Marker genes heatmap](results/Basic%20Scanpy%20Spatial%20Analysis/6.%20marker_genes_heatmap.png)
> *Figure 6. Heatmap of representative marker genes across clusters, showing differential expression patterns and similarity relationships among cluster identities.*

**Key observations**
- Marker genes show **cluster-specific expression patterns** across the dataset.
- Several clusters are enriched for genes such as **CR2, FDCSP, CLU, LRMP, and MEF2B**.
- The dendrogram suggests **transcriptional similarity among subsets of clusters**.
- Some clusters display strong multi-gene enrichment, indicating **distinct molecular identities**.
- These patterns support **cluster annotation using canonical or candidate marker genes**.

## 14. Plot a marker gene in space

A selected marker gene is visualized together with cluster labels to help interpret the biological identity of clusters.

![Spatial Clusters and CR2](results/Basic%20Scanpy%20Spatial%20Analysis/7.%20Spatial%20Clusters%20and%20CR2.png)
> *Figure 7. Spatial map of cluster assignments and CR2 expression across the tissue section, showing how marker expression relates to transcriptionally defined regions.*

**Key observations**
- CR2 expression is **spatially heterogeneous** across the tissue.
- Higher CR2 signal appears in **specific cluster-associated regions**.
- Expression is **localized rather than uniform**, suggesting cluster-restricted enrichment.
- The comparison supports **marker-based cluster annotation**.

## 15. Plot additional genes in space

Additional genes are plotted in tissue space to compare their spatial expression patterns across the sample.

![Spatial COL1A2 and SYPL1](results/Basic%20Scanpy%20Spatial%20Analysis/8.%20Spatial%20COL1A2%20and%20SYPL1.png)
> *Figure 8. Spatial expression of COL1A2 and SYPL1 across the tissue section, highlighting gene-specific localization patterns.*

**Key observations**
- Both genes show **spatially heterogeneous expression** across the tissue.
- **COL1A2** appears enriched in more localized regions, suggesting restricted spatial expression.
- **SYPL1** shows a broader but still non-uniform distribution.
- The differing patterns indicate **distinct biological roles or tissue-associated domains**.


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

![UMAP Clusters](results/Basic%20Scanpy%20Spatial%20Analysis/9.%20UMAP%20Clusters.png)
> *Figure 9. UMAP projection of spots/cells colored by cluster identity, showing the transcriptional structure of the dataset.*

**Key observations**
- The UMAP reveals **six distinct clusters** with varying degrees of separation.
- Some clusters are **well separated**, indicating strong transcriptional differences.
- Other clusters lie closer together, suggesting **related expression profiles** or gradual transitions.
- The projection supports the presence of **meaningful transcriptional heterogeneity** in the dataset.

![Spatial Cluster Map](results/Basic%20Scanpy%20Spatial%20Analysis/10.%20Spatial%20Cluster%20Map.png)
> *Figure 10. Spatial distribution of cluster identities across the tissue coordinates, illustrating how transcriptional clusters are arranged in physical space.*

**Key observations**
- The map shows **six spatially distributed clusters** across the tissue area.
- Some clusters form **localized neighborhoods**, while others are more dispersed.
- The mixed distribution suggests **spatial heterogeneity** rather than strict segregation.
- This view helps relate **transcriptional clustering to tissue organization**.

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

# Notebook 4: Xenium Spatial Transcriptomics Analysis

This notebook analyzes end-to-end spatial transcriptomics pipeline on 10x Genomics Xenium data. Covers QC, normalization, clustering, and spatial analysis — neighborhood enrichment, co-occurrence, and spatially variable gene detection — using `spatialdata`, `scanpy`, and `squidpy`.

---

## Overview

1. Mount Google Drive
2. Import Libraries
3. Set File Paths
4. Load Xenium Data
5. Extract AnnData Table
6. View Cell Metadata
7. View Spatial Coordinates
8. Compute QC Metrics
9. Check Negative Controls
10. Plot QC Distributions
11. Filter Cells and Genes
12. Normalize and Cluster
13. Visualize UMAP
14. Plot Spatial Clusters
15. Build Spatial Neighbor Graph
16. Compute Centrality Scores
17. Plot Centrality Scores
18. Create a Subsample
19. Access the Subsample
20. Co-occurrence Analysis
21. Neighborhood Enrichment
22. Plot Neighborhood Enrichment
23. Spatial Autocorrelation
24. Plot Selected Genes Spatially
25. Reload Data and Plot Genes One by One.

---

## Dataset Description

10x Genomics **Xenium in situ** dataset with subcellular spatial transcriptomics at single-cell resolution. Includes:

- Cell-by-gene expression matrix with targeted gene panel counts
- Spatial coordinates of segmented cell centroids in tissue space
- Cell metadata — cell area, nucleus area, transcript counts, control counts
- Negative control probes and codewords for background noise estimation

Stored in Xenium output directory format, loaded via `spatialdata-io` into a `SpatialData` object.

---

## Requirements

### Environment

Runs in **Google Colab** with Google Drive mounted. Dataset placed at `/content/drive/MyDrive/Xenium`.

### Dependencies

```bash
pip install spatialdata spatialdata-io scanpy squidpy matplotlib seaborn
```

### Package Roles

- `spatialdata` — unified spatial data container
- `spatialdata-io` — Xenium format reader
- `scanpy` — QC, normalization, clustering
- `squidpy` — spatial graph construction and spatial statistics
- `matplotlib` / `seaborn` — visualization

---

## Workflow

### 1. Mount Google Drive

Mounts Google Drive in Colab so the Xenium dataset can be loaded from Drive.

### 2. Import Libraries

Imports packages needed for data loading, QC, preprocessing, clustering, plotting, and spatial analysis.

### 3. Set File Paths

Defines path to the Xenium dataset directory.

### 4. Load Xenium Data

Loads Xenium output into a **SpatialData** object containing spatial elements and the expression table.

### 5. Extract AnnData Table

Retrieves the main cell-by-gene expression table as an **AnnData** object.

### 6. View Cell Metadata

Shows per-cell metadata such as transcript counts, cell area, and control counts.

### 7. View Spatial Coordinates

Displays spatial coordinates for each cell, used in spatial plots and graph construction.

### 8. Compute QC Metrics

Calculates standard QC metrics like total counts and number of detected genes per cell.

### 9. Check Negative Controls

Measures percentage of counts from negative control probes and codewords to assess background noise.

### 10. Plot QC Distributions

Plots key QC distributions to inspect sequencing depth, gene diversity, segmentation size, and nucleus-to-cell area ratio.

### 11. Filter Cells and Genes

Removes very low-count cells and rarely detected genes to reduce noise.

### 12. Normalize and Cluster

Stores raw counts, normalizes, log-transforms, reduces dimensionality, builds neighbor graph, computes UMAP, and identifies clusters via Leiden algorithm.

### 13. Visualize UMAP

Plots cells in UMAP space colored by QC metrics and Leiden cluster labels.

### 14. Plot Spatial Clusters

Shows how Leiden clusters are distributed across the tissue section.

### 15. Build Spatial Neighbor Graph

Creates a spatial graph from cell coordinates using Delaunay triangulation.

### 16. Compute Centrality Scores

Calculates graph-based centrality measures for each Leiden cluster.

### 17. Plot Centrality Scores

Visualizes spatial centrality metrics across all clusters.

### 18. Create a Subsample

Creates a random 50% subset of cells for faster downstream spatial analyses.

### 19. Access the Subsample

Stores the subsampled dataset in a separate variable for subsequent steps.

### 20. Co-occurrence Analysis

Computes and plots how often clusters appear near one another spatially, then visualizes cluster positions in tissue space.

### 21. Neighborhood Enrichment

Tests whether certain clusters are spatially enriched or depleted in each other's neighborhoods.

### 22. Plot Neighborhood Enrichment

Displays neighborhood enrichment heatmap alongside spatial distribution of clusters.

### 23. Spatial Autocorrelation

Computes Moran's I statistic to identify genes with spatially patterned expression across the tissue.

### 24. Plot Selected Genes Spatially

Plots spatial expression of selected genes to inspect where they localize in the tissue.

### 25. Reload Data and Plot Genes One by One

Reloads Xenium data with cells represented as circles and plots each selected gene individually if present in the dataset.

## References

[Scanpy spatial tutorial](https://scanpy-tutorials.readthedocs.io/en/latest/spatial/basic-analysis.html)

[Squidpy Visium fluorescence tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_fluo.html)

[Squidpy Visium H&E tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_visium_hne.html)

[Squidpy Xenium tutorial](https://squidpy.readthedocs.io/en/stable/notebooks/tutorials/tutorial_xenium.html)

[10x Genomics Xenium Human Lung Cancer Dataset](https://www.10xgenomics.com/datasets/xenium-ffpe-human-lung-cancer)
