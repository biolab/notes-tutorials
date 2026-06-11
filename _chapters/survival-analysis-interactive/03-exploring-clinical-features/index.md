---
title: 'Exploring Clinical Features'
---

We previously estimated the difference in survival between two cohorts on a Kaplan-Meier plot and manually identified the feature that led to cohorts with distinct survival characteristics. However, real world survival datasets often include more than just 3 features to choose from. This time we will be working with a larger, clinical dataset, and we will start by exploring its features manually — one at a time, exactly as we did with the dental fillings.

For this example let's use the **German Breast Cancer Study Group** data. The first two columns show the time and event. Specifically the Recurrence Free Survival Time, the time between the start of the study and the recurrence of cancer. The rest of the data is full of other clinical variables. Some of them categorical, like tumor grade, and other continuous ones, like the patient's age.


<WidgetIframe 
  src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/2f0e56aa-b31d-44d0-95fd-aa74899b5c66?hidden=footer,header&theme=Light" 
  height="600px" 
/>

We already know how to form and compare groups manually. For categorical features, we simply select the feature in the Kaplan-Meier widget. There are three categorical features to choose from: Tumor Grade, Menopausal Status, and Hormonal Therapy.

<FullWidth>
  <WidgetIframe 
    src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/9377c96e-3b43-42fd-bf25-054729894407?hidden=footer,header,survival-variables/event,survival-variables/time&theme=Light"  
    height="700px" />
</FullWidth>

### **Try this:** 

Group by **Menopausal Status**. Then switch to **Hormonal Therapy**. Optionally, plot the median survival time and the confidence intervals to get a better idea of the data.

<Question
  id="ex-ranking-q1"
  points={1}
  question="When grouping by Menopausal Status, what do the curves and the log-rank p-value tell you?"
  options={["Clearly separated curves, p-value below 0.05", "Curves are barely separated, p-value is large", "Pre-menopausal patients have a significantly worse prognosis"]}
  answer="Curves are barely separated, p-value is large"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Being in menopause doesn't really have much effect on recurrence-free survival; the curves are barely separated, and the p-value is quite large.

  </Explanation>
</Question>

<Question
  id="ex-ranking-q2"
  points={1}
  question="When grouping by Hormonal Therapy, which group has a significantly worse prognosis?"
  options={["Patients who received hormonal therapy", "Patients who did not receive hormonal therapy", "Neither — the difference is not significant"]}
  answer="Patients who did not receive hormonal therapy"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  The patients that did not receive hormonal therapy had a significantly worse prognosis. The p-value should be much smaller than for Menopausal Status.

  </Explanation>
</Question>

Using numeric features to form cohorts takes an extra step; we need to define a threshold to split the data. Say we're interested in whether there is a significant difference in survival between patients above and below the age of 60. The widget below lets you pick a numeric feature and slide the threshold.

<FullWidth>
  <WidgetIframe
    src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/588ec724-16fe-4f8b-b811-3add3b36fcc5?hidden=columns,distribution,header,footer&theme=Light"
    height="550px"
  />
</FullWidth>

<FullWidth>
<WidgetIframe
  src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/6748550b-4e73-4db0-8238-65a915358c62?hidden=survival-variables/event,survival-variables/time,header,footer&theme=Light"
  height="650px"
/>
</FullWidth>


### **Try this:** 

Set the feature to **Age** and the threshold to **60**. Then lower the threshold to **40**.

<Question
  id="ex-ranking-q3"
  points={1}
  question="Comparing the two age thresholds, which one separates the survival curves more clearly?"
  options={["Threshold at 60", "Threshold at 40", "Both look about the same"]}
  answer="Threshold at 40"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Whether a patient is above or below 60 doesn't make a big difference in the survival probability over the observed time. With the threshold at 40, there is a more significant difference between the survival curves.

  </Explanation>
</Question>

Switch the feature to **Progesterone receptor** and put the threshold in the lowest bin — it already contains more than half the patients.

<Question
  id="ex-ranking-q4"
  points={1}
  question="When splitting patients on progesterone receptor with the threshold in the lowest bin, what do you see?"
  options={["A striking difference between the two curves", "Curves are barely separated", "Curves overlap completely"]}
  answer="A striking difference between the two curves"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  This time we really see a big difference between the two survival curves. Progesterone receptor level is informative for recurrence-free survival in this cohort.

  </Explanation>
</Question>
