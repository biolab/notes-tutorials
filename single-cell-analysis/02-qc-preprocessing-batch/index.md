---
title: 'Quality Control, Preprocessing and Batch Effect Correction'
subTitle: ''
chapters: 
    - single-cell-analysis/04-preprocessing
    - single-cell-analysis/05-batch-effects
    - single-cell-analysis/quiz-02
--- 


**Why do we need to clean and adjust single-cell data before analysis? How can technical differences between experiments affect our results? In these chapters, we introduce basic steps for preparing single-cell datasets for analysis.**

We begin with filtering, where we remove low-quality cells and genes that do not provide useful information. This helps reduce noise in the data. We then apply preprocessing steps such as normalization and log transformation to make gene expression values comparable across cells. Finally, we look at batch effects—differences between datasets caused by technical factors—and show how to correct them so that data from different sources can be analyzed together.

Following are the main concepts we will cover:

- **Filtering (Quality Control):** Removing low-quality cells and uninformative genes.

- **Detection Count:** Measures how often something is observed, regardless of how strongly it is expressed.  
  - For a **gene**: in how many cells it appears (has a non-zero value).  
  - For a **cell**: how many genes are detected in that cell.

- **Total Count:** Measures how much expression is present overall.  
  - For a **gene**: the sum of its expression across all cells.  
  - For a **cell**: the total number of transcripts detected in that cell.

- **Normalization:** A preprocessing step that adjusts gene expression values to make cells comparable, usually by correcting for differences in the total number of detected transcripts in each cell.

- **Log Transformation:** Scaling values to reduce large differences.  

- **Batch Effects:** Non-biological differences between datasets caused by technical variation during data collection or processing.

- **Batch Correction:** Methods that adjust data to remove batch effects, allowing datasets from different sources to be compared and combined.

