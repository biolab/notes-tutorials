---
title: 'Beyond Survival Curves'
omitAsChapter: true
---

A few directions worth knowing about:

- **Cox proportional hazards regression.** Kaplan–Meier compares groups one feature at a time. The Cox model lets you fit several features together and estimate the effect of each *while holding the others fixed* — for example, the effect of tumor grade after adjusting for stage. This is the standard tool for adjusted survival analysis in biomedicine.
- **Confounding and multivariate adjustment.** As noted at the end of the previous module, simple two-group comparisons can mislead. As Clark et al. (2003) and Bradburn et al. (2003) put it: if one treatment group happens to be younger than the other, a naïve Kaplan–Meier might attribute better outcomes to the treatment when really age is doing the work. Multivariate models — Cox regression and its many extensions — exist to handle exactly this.
- **Beyond the proportional hazards assumption.** The Cox model assumes that the relative effect of a feature is constant over time. When it is not — for example, when a treatment helps in the short term but not the long term — there are more flexible alternatives (time-varying coefficients, parametric survival models, accelerated failure time models, random survival forests).
- **From clinical features to molecular biology.** We worked exclusively with clinical variables here. A natural next step is to bring in molecular data — gene expression, mutations, or summarized pathway activity scores — and ask which biological pathways influence survival, alone or after adjusting for clinical factors.

Survival analysis is one of those rare areas of statistics where the simple tools (Kaplan–Meier, log-rank) carry you a remarkably long way *and* the more advanced tools sit on the same intuitions. If the staircase-shaped curve makes sense to you, you have a solid foundation for everything else.
