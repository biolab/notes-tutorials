---
title: 'Exploring Survival Features'
subTitle: 'Forming and comparing groups.'
chapters:
    - survival-analysis/03-forming-and-comparing-groups
    - survival-analysis/04-ranking-survival-features
    - survival-analysis/quiz_02
---

**In this chapter, you will learn how to create groups of samples (subjects, patients) using additional features from the data set and how to assess whether these groups showcase a difference in survival. You will also learn how to automatically rank and find the data features that best correlate with survival.**

In survival analysis, we are often interested not just in how long something lasts, but in *why* it lasts longer in some cases than others. By exploring additional features in our dataset—like material type or brushing habits—we can form meaningful groups and compare their survival outcomes. This helps us uncover which factors might influence longevity. In this chapter, we will learn how to group data, compare survival curves, and identify the most informative features. We will cover the following concepts:

- **Categorical Feature**: A variable with distinct categories, like material type (ceramic or composite), used to form groups for comparing survival.

- **Continuous Feature**: A variable with a range of numeric values, like brushing time, requiring thresholds to split into groups.

- **Data Grouping**: The process of dividing data based on a feature to compare survival curves between subgroups.

- **Kaplan-Meier Curve**: A graph showing survival over time, used here to compare different groups based on selected features.

- **Log-Rank Test**: A statistical test that checks whether the difference between two survival curves is likely due to chance.

- **Threshold**: A chosen value used to split a continuous feature into two groups (e.g., brushing more or less than 6 minutes).

- **Feature Ranking**: Automatically evaluating which features best separate the data into groups with different survival outcomes.

- **P-Value**: A number indicating whether the difference in survival between groups is statistically significant (typically below 0.05).

- **Discretization**: Converting a continuous feature into categorical bins to enable group comparisons.


**Start by watching the following videos or if you prefer, you can skip them and start reading the lecture notes below.**

<YouTube embedId="b7Ll_X94Djk" />

<YouTube embedId="9KXteGhzNOY" />