---
title: 'Ranking Gene Sets'
subTitle: 'Ranking gene sets based on survival.'
chapters:
    - survival-analysis/06-ranking-gene-sets
    - survival-analysis/quiz_04
---

**There may be many, possibly hundreds of genes that affect survival. For interpretation purposes, it may be helpful to consider only groups of genes instead, such as genes from the same pathway. Here, we will learn how to evaluate the effect of a collection of genes on survival and how to rank gene sets according to their association with survival.**

In the previous sections, we explored breast cancer data and ranked the eight clinical features according to their effect on survival. Emerging data sets in biomedicine can include many more features though. For example, tissue samples are characterized by the expression of thousands of genes. We'll now learn how to explore such data according to survival, and cover the following concepts:


- **Gene Expression**: A measurement of how active a gene is in a given tissue, often used to study disease outcomes.

- **Bioinformatics**: A field that combines biology and computing, used here to analyze large-scale gene data.

- **Gene Set**: A group of genes linked by a common function or pathway, like the RAS signaling pathway that plays a key role in cell growth, proliferation, differentiation, and survival.

- **Recurrence-Free Survival**: Time from treatment until the cancer returns.

- **Overall Survival**: Time from treatment until death related to the disease.

- **Median Expression Split**: A method of forming groups based on whether a gene's expression is above or below its median value.

- **Feature Ranking**: Ordering genes (or features) by how well they separate survival outcomes.

- **Enrichment Score**: A metric that quantifies the collective expression of a gene set relative to the rest of the genes in a sample, used to estimate the activity level of a biological pathway.

**Please start by watching the following video or if you prefer, you can skip it and start reading the lecture notes below.**

<YouTube embedId="eQgBvXGuWY0" />
