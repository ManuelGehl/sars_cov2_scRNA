# sars_cov2_scRNA

## Data and Preprocessing

The data used in this project comes from human upper airway tissue, specifically the inferior turbinate and ethmoid sinus mucosa. It was obtained from the Broad Institute's Single Cell Portal with the accession number SCP253.
To manage the large dataset within available computational resources, the original dataset containing 45,101 barcodes was downsampled to 3,000 barcodes. This reduction was a crucial step to enable further analysis without overwhelming computational capacity.
Quality control (QC) indicated that the data was of excellent quality (**Fig. 1**)), suggesting it was prefiltered by the original authors. Only slight adjustments were necessary, including filtering out barcodes with more than 40% mitochondrial gene expression. This adjustment was made because the analysis focuses on epithelial cells, which generally have lower metabolic activity. Additionally, doublet detection suggested only three possible doublets, which were disregarded due to their minimal impact on the dataset's overall quality.

![Fig. 1](figures/qc_plot.png)


## Feature selection, dimensionality reduction, clustering, and cell annotation

Seurat was employed to identify the most variable genes within the dataset. This set of highly variable genes was then used to construct a Principal Component Analysis (PCA), enabling dimensionality reduction from the original large dataset.
Based on the first 30 principal components derived from the PCA, a neighborhood graph was constructed, serving as the foundation for subsequent analyses, including Uniform Manifold Approximation and Projection (UMAP).
The reduced-dimension UMAP was thoroughly examined to ensure there were no quality control issues. The inspection of QC parameters revealed no obvious problems, indicating that the dataset was suitable for clustering and further analysis.
Clustering was performed using the Leiden algorithm. The optimal resolution was determined to be 0.25, providing a balance between the number of clusters and the granularity of the analysis.
For cell annotation, Celltypist was used with the "Human_Lung_Atlas" model to categorize the clusters identified by the Leiden algorithm. This automated annotation process yielded several confidently annotated clusters, including Mast cells, multiciliated cells, CD8 T cells, plasma cells, submucosal gland cells (SMG), and goblet cells (**Fig. 2**). These annotations were consistent with the expected cell types and aligned well with the results from the original publication.

![Fig. 2](figures/umap_predictions.png)
