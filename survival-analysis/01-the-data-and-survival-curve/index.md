---
title: 'The Data and Survival Curve'
subTitle: 'A gentle introduction to survival analysis.'
chapters:
    - survival-analysis/01-survival-data
    - survival-analysis/02-survival-curves
    - survival-analysis/quiz_01
---


**What is special about survival data? What is censoring? How do we visually represent changes in survival probabilities over time? In this chapters, we will go through some basic concepts of survival analysis. We will work with a toy example of survival data and show how to plot the survival curve, one of the key visualizations in survival analysis.**


Understanding how long something lasts before an event occurs—be it a machine breaking down, a product failing, or a dental filling falling out—is at the heart of survival analysis. Unlike standard statistical methods that expect a complete outcome for every case, survival analysis is uniquely suited to handle incomplete information through the concept of censoring. Here we will introduce survival data, explain how to prepare it for analysis, and demonstrate how to visualize time-to-event outcomes using the survival curve. Through a relatable example involving dental fillings, we’ll explore how to handle censored observations and estimate survival probabilities with tools like the Kaplan-Meier estimator—both manually and using the Orange data mining platform. Following are main concepts that we will cover:

- **Survival Analysis**: A way to study how long it takes for something to happen.

- **Event**: The outcome we are observing, like a dental filling falling out.

- **Censoring**: When the event hasn’t (yet) happened during the study or its timing is unknown.

- **Survival Time**: The time from the beginning of observation until the event or censoring.

- **Kaplan-Meier Curve**: A graph showing the chance of the event not happening over time.

**Start by watching the following video or if you prefer, you can skip it and start reading the lecture notes below.** 

<YouTube embedId="kWWcZ3sBtuE" />
