---
title: 'Ranking Survival Features'
---

We previously estimated the difference in survival between two cohorts on a Kaplan-Meier plot and manually identified the feature that led to cohorts with distinct survival characteristics. However, real world survival datasets often include more than just 3 features to choose from. This time we will be working with a larger dataset. We will start by exploring the features manually. Then, we will let Orange do some of the work for us. 

We can find the available survival datasets in Orange using the [Dataset](https://orangedatamining.com/widget-catalog/data/datasets/) widget. Just type "survival" into the search bar. For this example let’s use the German Breast Cancer Study Group data. Select the dataset and conenct it to the [Data Table](https://orangedatamining.com/widget-catalog/data/datatable/) widget. The first two columns show the time and event. Specifically the Recurrence Free Survival Time, the time between the start of the study and the recurrence of cancer. The rest of the data is full of other clinical variables. Some of them categorical, like tumor grade, and other continuous ones, like the patient's age. Note, we dont use [As Survival Data](https://orangedatamining.com/widget-catalog/survival-analysis/as-survival-data/) widget here because this dataset is already in the correct format for survival analysis.

![](04-load-dataset.png)

We already know [how to form and compare groups](/books/survival-analysis-tutorial#forming-and-comparing-groups) manually. For categorical features, we simply pass the data to the [Kaplan-Meier](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/) widget. There are three categorical features to choose from: Tumor Grade, Menopausal Status, and Hormonal Therapy.

![](04-km-categorical-variables.png)

<!!! float-aside !!!>
A p-value below 0.05 indicates that there is a significant difference between the survival curves.

Let's try Menopausal Status and Hormonal therapy. Also, let's plot the median survival time and the confidence intervals to get a better idea of the data. We find that being in menopause doesn't really have much effect on survival; the curves are barely separated, and the p-value is quite large. What about Hormonal therapy? This, on the other hand, is very informative. The patients that did not receive hormonal therapy had a significantly worse prognosis.

<!!! width-max !!!>
![](04-km-plots.png)

Using numeric features to form cohorts takes an extra step; we need to define a threshold to split the data. In the [previous section](/books/survival-analysis-tutorial#forming-and-comparing-groups) we used [Select rows](https://orangedatamining.com/widget-catalog/transform/selectrows/) for this, but this time we do this with the [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) widget. Say we're interested in whether there is a significant difference in survival between patients above and below the age of 60. In the [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) widget, change the bin width to a small number. Five will do. Then select the population above the age of 60 by interactively selecting bins.

<!!! float-aside !!!>
The [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) widget allows us to define groups by interactively selecting a part of a feature's distribution.

![](04-distributions.png)

To see what we’ve done we’ll use the [Data Table](https://orangedatamining.com/widget-catalog/data/datatable/) widget. The default output of the [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) widget is only the selected data; in our case, this means only the patients above 60. But we want all the patients, so we have to rewire the connection. After rewiring we can see that the [Data Table](https://orangedatamining.com/widget-catalog/data/datatable/) has an extra column called "Selected" that specifies the group.

<!!! float-aside !!!>
Remember, Orange widgets can have different outputs. When we select a part of an interactive visualisation only the selected part of the data is passed on. If we wish to compare the selected part of the data to the non-selected one, we have to rewire the connection and pass on all the data.
![](04-rewire-connection.png)

![](04-distributions-table.png)

Now we can send the data from [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) to [Kaplan-Meier](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/) widget. It turns out that whether a patient is above or below 60 doesn’t make a big difference in the survival probability over the observed time.

<!!! width-max !!!>
![](04-distributions-kmplot.png)

We can also try different thresholds now that we have constructed our workflow. For example, let's select everyone over the age of 40 in [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/). You can see that Orange automatically reflects this change in the plot. And there is a more significant difference between the survival curves now.

<!!! width-max !!!>
![](04-distributions-kmplot-over40.png)

<!!! float-aside !!!>
The survival curve of the selected group is always red. Furthermore, the selected group can be above the threshold (e.g., above a certain age) or below it (e.g., below a certain progesterone receptor value).

Next, we can try another continuous variable like the Progesterone receptor. Let's select just the first bin since it already contains more than half the patients. This time we really see a big difference.
<!!! width-max !!!>
![](04-distributions-kmplot-prog-receptor.png)

To make comparing features easier, we can use the [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/) widget, which forms cohorts for each variable and evaluates their difference in survival using the log-rank test. So let's send our data to [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/). There's a selection of two scoring methods for establishing which feature is most predictive of survival. Orange automatically selects the multivariate log-rank test, and we'll stick with that. Next, we can sort the features by p-value; we find the most informative is the Number of Positive Nodes. Positive nodes refer to lymph nodes in the armpit area where metastatic cancer cells have been found.

<!!! float-aside !!!> 
The [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/) widget uses the median value as a threshold for the continuous features.

![](04-ranking.png)

<!!! float-aside !!!> 
On the left of the [Discretize](https://orangedatamining.com/widget-catalog/transform/discretize/) widget, we select the feature we want to split by, and on the right, we tick the option to split by equal frequency intervals. Notice that the red survival curve corresponds to the group above the median of a given continuous feature.

We can inspect what the survival curve actually looks like in this case. The output of the [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/) widget is a reduced dataset containing the time and event columns along with the selected feature. So we can choose "Number of Positive Nodes," and then we need to split the data at the median again. We could do this via [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/), like before, or as an alternative, we could use the [Discretize](https://orangedatamining.com/widget-catalog/transform/discretize/) widget. So let's connect them and split our data into two intervals of equal frequency. Now we can connect this to another [Kaplan-Meier](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/) widget, and there we go. We successfully identified the most informative feature regarding survival just with a few clicks.

<!!! width-max !!!>
![](04-ranking-reduced.png)
