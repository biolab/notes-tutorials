---
title: 'Ranking Survival Features'
---

Up until now we have been forming and comparing groups by hand — one feature at a time, picking thresholds ourselves. That works when there is only a handful of clinical variables to consider, but real survival datasets often include dozens, and molecular datasets reach into the thousands. To explore at that scale we need a more systematic way of asking the same question — *does this feature separate survival?* — for every feature at once.

<!!! float-aside !!!>
The Rank Survival Features widget uses the median value as a threshold for the continuous features.


Let's look at the **Rank Survival Features** widget, which forms cohorts by splitting samples at the median value for continuous features (and by category for categorical features), then evaluates the difference in survival between those cohorts using the log-rank test. There's a selection of two scoring methods for establishing which feature is most predictive of survival; we'll stick with the multivariate log-rank test.


<FullWidth>
  <div style={{ display: "flex", gap: "16px", width: "100%" }}>
    <div style={{ width: "calc(40% - 2px)", minWidth: 0 }}>
      <WidgetIframe src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/286831a5-6e62-4f8f-90c3-8eca7fb21426?hidden=sidebar,header,footer&theme=Light&code=wooden-screw-68" height="700px" />
    </div>

    <div style={{ width: "calc(60% - 2px)", minWidth: 0 }}>
      <WidgetIframe src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/ccb9b5e4-dc15-48e3-985c-6d1673292684?hidden=sidebar,footer,header&theme=Light&code=wooden-screw-68" height="700px" />
    </div>
  </div>
</FullWidth>

### **Try this:** 

Sort the features by p-value, then click on the top-ranked one. The Kaplan-Meier curve appears below — patients split at the median, with the above-median group in red. Then click through the other features in order of p-value and compare the gaps.

<Question
  id="ex-ranking-q5"
  points={1}
  question="Which clinical feature ranks first by log-rank p-value?"
  options={["Age", "Hormonal Therapy", "Number of Positive Nodes", "Tumor Grade"]}
  answer="Number of Positive Nodes"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Sorted by p-value, the most informative feature is the Number of Positive Nodes. Positive nodes refer to lymph nodes in the armpit area where metastatic cancer cells have been found — one of the oldest and strongest prognostic markers in breast cancer.

  </Explanation>
</Question>

<Question
  id="ex-ranking-q7"
  points={1}
  question="Look at the Kaplan-Meier curve for the top-ranked feature. The above-median group is shown in red. Do patients with a higher number of positive lymph nodes have better or worse recurrence-free survival?"
  options={["Better — higher node count means longer time to recurrence", "Worse — higher node count means faster recurrence", "No difference — node count does not affect recurrence"]}
  answer="Worse — higher node count means faster recurrence"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  The red curve (patients with above-median positive node counts) drops much faster than the curve for patients at or below the median. More involved lymph nodes mean more advanced metastatic spread, which translates to a shorter time to recurrence — a worse prognosis.

  </Explanation>
</Question>

<Question
  id="ex-ranking-q6"
  points={1}
  question="A small log-rank p-value tells you that the difference between groups is unlikely to be due to chance. Does it also tell you the feature is biologically important, causal, or large in effect size?"
  options={["Yes — a small p-value implies all of these", "No — those are separate questions and require additional analysis", "Only if the p-value is below 0.01"]}
  answer="No — those are separate questions and require additional analysis"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  A small p-value tells you the difference is unlikely to be chance. It does *not* by itself tell you that the feature is biologically important, causal, or large in effect size. Keep these separate in your head.

  </Explanation>
</Question>

We successfully identified the most informative feature regarding survival just with a few clicks.
