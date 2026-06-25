---
title: 'Survival data and the survival curve'
---



<!!! float-aside !!!>
Survival analysis is a set of techniques used for modeling time to an event of interest.

In survival analysis, the primary outcome we are interested in is the **time to an event of interest**. Each subject contributes two pieces of information: a **survival time** — a continuous value measured in days, months, or years — and an **event indicator** that records whether the event actually happened. The "survival" in survival analysis stems from its use in the study of the survival of patients. However, the event of interest can be many things: a disease relapse, the first technical failure of a car, or something as simple as the time until a newly acquired dental filling falls out. Many analysis methods would apply if the event occurred in all individuals. However, it is usual that at the end of a study, some individuals have yet to have the event of interest, and some might have ended their participation in the study beforehand for reasons other than experiencing the event. This doesn't mean that they won't necessarily experience the event in the future, but that their actual time to the event is unknown. This phenomenon is called **censoring**, and the data with an unknown true time to event is called **censored data**. Survival analysis includes a set of methods that can deal with datasets that include censored data. 

**Quick check.**

<Question
  id="warmup-1"
  points={1}
  question="Survival analysis refers to a set of statistical techniques used to analyze data where the outcome variable is the time until an event's occurrence."
  scorer={(answer) => answer.toLowerCase() === "true"}
  options={["True", "False"]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  True. Survival analysis is exactly this family of methods: the outcome it models is the time until an event — a death, a relapse, or a filling falling out — occurs.

  </Explanation>
</Question>

<Question
  id="warmup-2"
  points={1}
  question="Survival data records two things for each subject. Which pair is it?"
  options={[
    "A continuous survival time and a binary event indicator",
    "Two continuous measurements",
    "Two binary indicators",
  ]}
  answer="A continuous survival time and a binary event indicator"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Each subject contributes a continuous **survival time** (how long until the event or until we lose track of them) paired with a binary **event indicator** (1 if the event happened, 0 if the observation was censored). The other options miss this time-plus-event structure.

  </Explanation>
</Question>

<!!! float-aside !!!>
Data with an unknown true time to event is called censored data.

Let's look at the example from the videolecture. We gathered from a group of 10 friends when they last got a dental filling in the last ten years and when it fell out if it did. Can we estimate the probability of a new dental filling remaining in place after five years?

Below we plotted the answers as a diagram. The x-axis marks the time from 2012 to 2022, and the lines represent when each person got their dental filling and how long it lasted. For instance, Bert got a dental filling in 2012, which lasted until 2015, and Fay got her's in 2014, which lasted until 2020. We have marked the friends whose dental filling fell out with a cross. However, two of the participants in this small study, Irene and Chloe, had their dental filling in place at the end of our observation window. And Harry and Fay did not lose their dental fillings, but for some reason or another, we do not know what happened to their dental fillings from 2020 to 2022. Perhaps they got them changed before the fillings had the chance to fall out. These four participants represent our censored data points. The time their dental fillings stayed in place still tells us something about how long fillings usually last. So instead of discarding their data, we mark them with a circle.

![](01-diagram-1.png)

This data represents an example of right censoring, but we also know cases with left- and interval censoring. Left-censoring would mean that we observe the presence of a state or condition but do not know when it began. Interval censoring, on the other hand, means that individuals come in and out of observation. This tutorial focuses only on right-censoring since this is how most survival data is censored.

**Quick check.**

<Question
  id="warmup-4"
  points={1}
  question="If an individual has not experienced the event before the study ends, their survival time is considered censored."
  scorer={(answer) => answer.toLowerCase() === "true"}
  options={["False", "True"]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  True. If the event hasn't occurred by the end of observation, we don't know the true event time — only that it is longer than the time we observed. That is right-censoring.

  </Explanation>
</Question>

A minimal survival dataset is thus composed of observations with a survival time and event variable. The latter specifies if the event has, in fact, occurred (event=1) or whether it has been censored (event=0). We can transform our dental fillings data plotted as a diagram into a data table suitable for survival analysis. Since we are interested in how much time the dental filling lasted and not exactly what year it fell out, we re-plot the diagram, aligning when each person got their cavity filled to time 0.

![](01-diagram-2.png)

We can now easily transform this diagram into a data table. We order the data instances by time so that Anthony - whose time to his filling falling out is the shortest - is first, Bert is second, followed by Chloe, and so on. The third column contains the data on event censoring. On the diagram, we've marked Anthony and Bert with a cross, which means their filling fell out. Under their names in the table, we input a 1. But Chloe is marked with a circle since her filling has yet to fall out by the end of 2022, so we input a 0. We do the same for others. We have successfully prepared the data for the application of survival analysis methods.

**Quick check.**

<Question
  id="warmup-3"
  points={1}
  question="The occurrence of an event is typically described by a binary variable with values of 0 or 1."
  scorer={(answer) => answer.toLowerCase() === "true"}
  options={["True", "False"]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  True. The event indicator is binary: 1 means the event was observed (the filling fell out), 0 means the observation was censored.

  </Explanation>
</Question>


<WidgetIframe
  src="https://lab.orangedatamining.com/embed/5103afe3-dae2-46b7-86ef-48d04c2b68a5/32aaedaa-cabd-402f-9370-6dee5fee37f6?hidden=footer,header&theme=Light&code=important-procedure-74"
  height="400px"
/>

<!!! float-aside !!!>
The survival function gives the probability of surviving past a particular time.

We now have the data nicely organized. Back to our original question: *how likely is a new dental filling to stay in place after five years?*

Intuitively, the probability of this happening **increases over time** because minor damages to and around the dental filling accumulate as time goes by. These damages can be due to the *type of filling and its interaction with the bacterial biofilm, your diet, saliva composition, mechanical forces*, etc. However, when we visually represent such data, we want to plot the probability of **the event not happening**. In this case, the probability of the dental filling *not falling out*. To put it a bit crudely, we are interested in the probability of it **surviving in your mouth as time passes**. 

We can estimate the **survival function** - *the probability of surviving past a particular time* - using the **Kaplan-Meier estimator**. Let's calculate the survival probability and its changes over time *by hand*.

## Computing the curve, step by step

On the x-axis, we mark the time in years, and on the y-axis, the probability of the dental filling staying in place. Assuming the dentist did a good job, the probability of the filling being in place at time zero is exactly 1. Everyone walks out of the clinic with their filling intact.

<ReplayImg src="survival_curve.svg" alt="Animation" />

- **Years 0–2.** No one loses their filling in the first two years. The probability stays at 1.
- **Year 2.** Anthony's filling falls out. One out of ten people who were *at risk* loses their filling, so the survival probability drops by a factor of 1/10. The new probability is 0.9.
- **Years 2–3.** Nothing else changes. The curve stays flat at 0.9.
- **Year 3.** Bert's filling falls out, and Chloe is censored. At this point Anthony has already failed, so nine people are at risk. The probability of staying in place *given that you made it to year 3* is 1 − 1/9 ≈ 0.89. Survival is cumulative, so we multiply by the previous value: 0.89 × 0.9 ≈ 0.8.
- **Years 3–4.** Flat again at about 0.8.
- **Year 4.** David and Elle both lose their fillings. How many were at risk going into year 4? We started with 10. Anthony failed at year 2; Bert failed at year 3; and Chloe — although she did *not* fail — was censored at year 3, so she leaves the at-risk pool too. That leaves seven people at risk. Two of them fail, so the local survival probability is 1 − 2/7. Multiply by the running value: (1 − 2/7) × 0.8 ≈ 0.57.

Notice what happened with Chloe. She did not fail, but the fact that she was *censored* — that we lost track of her — removed her from the denominator. That is how Kaplan–Meier folds censored observations into the calculation without either discarding them or counting them as failures.


<Question
  id="ex-shorter-observation-window-gabe"
  points={1}
  question="In the full diagram, Gabe's filling falls out after about 7 years. Now suppose the study had ended at the end of 2020, when Gabe had only been observed for about 6 years. How would Gabe's row change?"
  options={[
    "Gabe would be censored at about 6 years",
    "Gabe would still be recorded as an event at about 7 years",
    "Gabe would be removed from the dataset",
  ]}
  answer="Gabe would be censored at about 6 years"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  If the study ends before the filling falls out, we do not observe the event in that study window. Gabe still contributes follow-up time up to the cutoff, but his event indicator would be 0.

  </Explanation>
</Question>

<Question
  id="ex-shorter-observation-window-meaning"
  points={1}
  question="More generally, what happens when we shorten the observation window from 2022 to 2020?"
  options={[
    "Some later events become censored observations",
    "All survival times stay the same",
    "Censored observations become observed events",
  ]}
  answer="Some later events become censored observations"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Shortening the study means we stop watching earlier. Events that happen after the cutoff are not observed as events in that dataset. Those subjects still contribute information up to the cutoff, but their event indicator is 0.

  </Explanation>
</Question>



<!!! float-aside !!!>
The Kaplan–Meier plot is a visual representation of the survival function.

We make these small calculations for the rest of the time points and draw the steps until we reach the end of our 10-year observation window. The graph we have produced is the Kaplan-Meier plot, which is one of the most used plots in survival analysis. It shows us how the survival probability changes over time. 

**Quick check.**

<Question
  id="ex-curve-meaning"
  points={1}
  question="The Kaplan–Meier curve plots the probability that the event has already happened by a given time."
  scorer={(answer) => answer.toLowerCase() === "false"}
  options={["True", "False"]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  False. The curve plots the probability of *surviving past* a given time — the probability that the event has *not* happened yet. It starts at 1 and steps downward as events occur.

  </Explanation>
</Question>

<!!! float-aside !!!>
The survival median is the time at which the survival probability drops to 0.5.

So, for instance, if we want to know the time at which the survival probability drops to 0.5, we can read it on the plot. Look for the point where the curve has fallen to 50% and note the corresponding time on the x-axis. In the literature, this time, called the survival median, is often marked on the Kaplan-Meier plot.

Doing the calculation by hand once builds intuition. After that, we let a computer do the arithmetic. Below is the same ten-friends dental fillings dataset loaded into the **Kaplan–Meier** widget. The curve should be identical to the one we worked out in the previous steps. Interact with the widget to confirm if the curve and calculated statistics match what you got by hand.

**Try this - interact with the widget to confirm if the curve and calculated statistics match what you got by hand.**

<FullWidth>
  <WidgetIframe
    src="https://lab.orangedatamining.com/embed/5103afe3-dae2-46b7-86ef-48d04c2b68a5/eefa1b23-f78a-45f1-81e4-58bf7276f341?hidden=sidebar,header,footer&theme=Light&code=important-procedure-74"
    height="800px"
  />
</FullWidth>

<Question
  id="ex-median-survival"
  points={1}
  question="What is the median survival time for the dental fillings?"
  options={["7 years", "5 years", "10 years"]}
  answer="7 years"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  The median survival time is the point where the survival probability drops to 0.5. Reading off the curve, that happens at seven years — half of the fillings are expected to have fallen out by then.

  </Explanation>
</Question>


## Takeaway

Survival data is special because it is almost always incomplete: at the end of any study, some individuals have not yet had the event. **Censoring** is the name for that partial information, and it is information — not missing data. The **Kaplan–Meier estimator** uses both events and censored observations to estimate the probability of surviving past each point in time.

The story works just as well when "friends and fillings" becomes "patients and tumors," which is where the next module picks up.
