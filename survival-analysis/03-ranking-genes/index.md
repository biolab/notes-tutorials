---
title: 'Ranking Genes'
subTitle: 'Ranking genes based on survival.'
chapters:
    - survival-analysis/05-ranking-genes
    - survival-analysis/quiz_03
---


**What if our data contains thousands of features, for example, as is the case in some molecular biology datasets? How do we approach survival analysis in such cases? Here, you will learn how to use gene expression data for survival analysis. We will show you how to identify genes that are most predictive of survival.**

In previous chapters, we explored breast cancer data and ranked the eight clinical features according to their effect on survival. Emerging data sets in biomedicine can include many more features though. For example, tissue samples are characterized by the expression of thousands of genes. We'll now learn how to explore such data according to survival, and cover the following concepts:

- **Gene Expression**: A measurement of how active a gene is in a given tissue, often used to study disease outcomes.

- **Bioinformatics**: A field that combines biology and computing, used here to analyze large-scale gene data.

- **Gene Set**: A group of genes linked by a common function or pathway, like the RAS signaling pathway that plays a key role in cell growth, proliferation, differentiation, and survival.

- **Recurrence-Free Survival**: Time from treatment until the cancer returns.

- **Overall Survival**: Time from treatment until death related to the disease.

- **Median Expression Split**: A method of forming groups based on whether a gene's expression is above or below its median value.

- **Feature Ranking**: Ordering genes (or features) by how well they separate survival outcomes.


**Please start by watching the video below or if you prefer, you can skip it and start reading the lecture notes below.**

<YouTube embedId="hk-lWB-ozd8" />