---
title: 'Forming and Comparing Groups'
---

**Besides the survival time and event information, observations in a survival dataset are often characterized with a feature or two. We can use the features to form groups and compare their survival curves. Forming groups differs whether the feature is categorical or continuous.**

Returning to our previous example, we have expanded the dental fillings dataset to include 10 more samples and three additional features.

The first additional feature concerns the type of material out of which the dental filling was made of. It turns out they were either composite or ceramic, so type of material is a categorical feature. Anthony got a composite filling, and so did Bert, however, Chloe got a ceramic one and so on. The second additional feature is named Brushing time and denotes the average amount of time in minutes someone spends brushing their teeth daily. Anthony uses an electric toothbrush, so he's timed his brushing to 4 minutes daily, while Bert says he takes a bit more time. Chloe, on the other hand, has braces and thus spends 15 minutes per day brushing her teeth. Brushing time is a numeric feature, meaning its values are continuous. Lastly, there is another categorical feature, this one denoting whether the subject of the study prefers cats or dogs.

**See the table below:**

<WidgetIframe
  src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/3b7437fb-1079-4011-bc3f-747761bdb183?hidden=header,footer&theme=Light&code=important-procedure-74"
  height="600px"
/>

<!!! float-aside !!!>
To form groups based on a categorical feature, we split participants based on the category to which they belong.

When we have a categorical feature, such as the type of material, it's easy to form groups of data instances. In our case, one group were friends with ceramic filling, and the other friends with composite filling. We can draw two survival curves on the same plot, each one corresponding to the filling type.


<FullWidth>
  <WidgetIframe
    src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/da6c5f69-0201-407e-9131-bceefc187f18?hidden=footer,sidebar,header&theme=Light&code=important-procedure-74"  
    height="700px"
  />
</FullWidth>


<Question
  id="ex-forming-q1"
  points={1}
  question="Which group does better, ceramic or composite?"
  options={["Ceramic", "Composite", "No visible difference"]}
  answer="Ceramic"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  The survival curve for the ceramic group stays higher than the composite curve over the observed time. Ceramic dental fillings have a better prognosis of staying in place than composite ones.

  </Explanation>
</Question>

<Question
  id="ex-forming-q2"
  points={1}
  question="How many participants are in the composite group, and what is its median survival time?"
  options={["10 participants, median 5 years", "8 participants, median 5 years", "10 participants, median 7 years"]}
  answer="10 participants, median 5 years"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>

  <Explanation after="attempt">
  Hint: Check the legend and look for the composite group row.

  The legend reports the number of non-censored observations out of all the participants within a group (e.g., 8/10 for the group with the composite filling) and the median survival time for each group (5 years for the group with the composite filling).

  </Explanation>
</Question>

<!!! float-aside !!!>
To form groups based on a continuous feature, we have to define a threshold and split participants based on that threshold.

On the other hand, if we want to group by a continuous feature we have to define a threshold value to form groups. We will form two groups, one whose members brush their teeth more than six minutes a day, and the other one whose members brush less than that. 

### **Try this:** 

Below, set the threshold to **brushing time > 6 minutes**. Then use the Kaplan-Meier widget and group by the newly created feature (called 'Selected'). Two curves should appear — one for those that brush more than 6 minutes a day, one for those that brush less. Feel free to experiment with different thresholds and see how the curves change.

<FullWidth>
    <WidgetIframe src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/e22b3fab-0443-4335-82d1-418ed45a838e?hidden=footer,header&theme=Light&code=important-procedure-74" 
    height="300px" />
    <WidgetIframe src="https://lab.orangedatamining.com/embed/7b29d5d3-b56f-4526-b6d9-3019d69c8fda/dbe0bafe-cdba-4597-bdea-6f870b3b873d?hidden=display,footer,header&theme=Light&code=important-procedure-74"  h
    eight="700px"/>
</FullWidth>


<Question
  id="ex-forming-q3"
  points={1}
  question="Compared with grouping by type of material, which feature made a more considerable difference in the survival curves by visual inspection?"
  options={["Type of material", "Brushing time", "Both showed a similar difference"]}
  answer="Type of material"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  Grouping the subjects of our study by material type made a more considerable difference in the survival curve than grouping by brushing time. We gathered this just by visually inspecting the data.

  </Explanation>
</Question>

Of course, it doesn't make sense to use just any feature to form groups. Not all features affect survival, so not all of them will separate the data into groups with different survival curves. For instance, one can assume that whether a person prefers dogs to cats does not affect how long their dental filling lasts. We can check this by forming groups by the last feature which contains information on whether the person prefers cats or dogs. The survival curves are barely separated. Preferring dogs to cats really doesn't affect the survival of dental fillings.

Switch the grouping variable to **cats or dogs**.

<Question
  id="ex-forming-q4"
  points={1}
  question="How separated are the survival curves when grouping by cats-vs-dogs preference?"
  options={["Clearly separated, similar to type of material", "Barely separated", "More separated than type of material"]}
  answer="Barely separated"
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">

  The survival curves are barely separated. Preferring dogs to cats really doesn't affect the survival of dental fillings — not every feature in a dataset will separate the data into groups with different survival outcomes.

  </Explanation>
</Question>

<!!! float-aside !!!>
To evaluate the difference between survival curves we use the log-rank test.

Although visual inspection is a useful way of exploring the data, there is of course a more systematic way of comparing how well a particular feature separates the survival curves which is called the [**log-rank test**](https://www.wikiwand.com/en/Logrank_test). It computes how likely the difference between survival curves is not random. The smaller the p-value, the more likely our feature actually separates the data into groups with different survival outcomes. We can see this value next to the Kaplan-Meier plot. Grouping by type of material gives us a smaller p-value.
