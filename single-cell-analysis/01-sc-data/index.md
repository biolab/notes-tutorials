---
title: 'Single-Cell Expression Data'
subTitle: ''
chapters: 
    - single-cell-analysis/01-introduction
    - single-cell-analysis/02-sc-data
    - single-cell-analysis/03-visualisation
    - single-cell-analysis/quiz-01
--- 

**What does it mean to study gene expression at the level of individual cells? How is single-cell data structured, and how can we make sense of such high-dimensional information? In these chapters, we introduce the basic concepts of single-cell transcriptomics and guide you through the process of exploring and visualizing single-cell data.**

We begin by contrasting single-cell expression analysis with traditional bulk approaches, highlighting why cell-level resolution is crucial for understanding biological variability. We then examine how single-cell datasets are organized, focusing on count matrices, metadata, and common features such as sparsity and dropout. Finally, we explore methods for visualizing high-dimensional data, using techniques such as PCA and t-SNE to uncover patterns and structure in cellular populations. Throughout the tutorial, we will work with example datasets and use the Orange data mining platform to perform the analysis in an intuitive, visual workflow.

Following are the main concepts we will cover:

- **Expression Profile:** A representation of gene activity in a single biological sample, such as a tissue or an individual cell.

- **Count Matrix:** A table of gene expression values across samples.

- **Count:** The number of times RNA from a specific gene is detected in a single cell.

- **Dropout:** The phenomenon where a gene is actually expressed in a cell but is not detected in the data, resulting in a recorded value of zero.

- **Sparse Data:** Data in which most values are zero (or missing), and only a small fraction of entries contain non-zero values.

- **Dimensionality Reduction:** Techniques used to visualize complex data in fewer dimensions.  

- **PCA (Principal Component Analysis):** A linear method that reduces dimensionality by capturing the main sources of variation in the data.  

- **t-SNE (t-distributed Stochastic Neighbor Embedding):** A non-linear method that groups similar cells together in a low-dimensional space, emphasizing local structure.


**Start by reading the lecture notes below and then answer the quiz questions.**

