---
title: 'Ranking genes'
---

For our analysis, we will need to install the Bioinformatics Add-On, which is available in the Options menu. Orange needs to restart after installing an add-on. We will explore the [METABRIC study](https://www.cbioportal.org/study/summary?id=brca_metabric), which includes the survival data of 1904 patients with primary breast tumors. Each patient sample is characterized by 35 clinical features and the expression of over 24 000 genes. We can take a quick look in the [Data Table](https://orangedatamining.com/widget-catalog/data/datatable/) widget. Scrolling to the right, we can see the clinical features and the thousands of gene expression values. We also find the data appropriately includes the Time and Event marked as target features. However, there are two more Time and Event columns marked as meta-features. This is because, in this study, they measured the recurrence-free survival time as well as the overall survival. Recurrence-free survival time refers to the time until cancer recurrence, and overall survival refers to the time until breast cancer-related death. We will use the [As Survival Data](https://orangedatamining.com/widget-catalog/survival-analysis/as-survival-data/) widget to specify which time and event pair we want to explore. Let’s select overall survival.


<!!! float-aside !!!> 
Note that survival datasets can have more than one Time and Event feature. Use [As Survival Data](https://orangedatamining.com/widget-catalog/survival-analysis/as-survival-data/) to select the appropriate pair.

![](051-dataset.png)

If we want to use the bioinformatics widgets on some dataset of genes, we have to pass the data through the [Genes](https://orangedatamining.com/widget-catalog/bioinformatics/genes/) widget. This will match the names of genes with the [NCBI Gene database](https://www.ncbi.nlm.nih.gov/gene/) and annotate the data with the appropriate gene codes. The first time you use this widget, it will have to load all the data from the server, which may take a few moments. Now that we’re done, we can see that each gene has an ID and a short description. From 24000 genes, the widget matched 18000, so we will be working on a slightly reduced dataset.

![](052-genes.png)

With these many features, you might wonder, how do we analyze all of this data? Many biomedical researchers are focused on finding genes that could be used for cancer prognosis. For example, breast cancer researchers have identified the proto-oncogene KRAS as an important factor. An [article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6933029/) reported that high expressions of KRAS are linked to significantly worse projections for patients in the METABRIC study. Let’s try reproducing one of the Kaplan-Meier plots from this report in Orange.

Gene expression values are continuous. We already know that this means defining a threshold to form groups to compare survival. We can again do this with the [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) widget. On the left, we filter the features to find KRAS and then adjust the bin width. The gene expression values in this data set are normalized, so we’ll select the values above 0. This should split the data more or less in half. We can connect [Distributions](https://orangedatamining.com/widget-catalog/visualize/distributions/) to the [Kaplan-Meier Plot](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/) and rewire the connection to pass on all the data. In the [Kaplan-Meier](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/) widget, we choose Selected for the group indicator and tick the boxes to display the confidence intervals and the median. The p-value below 0.005 indicates that there is indeed a significant difference in the survival curves between patients with KRAS expression above or below 0. The ones we selected on the Distributions graph, those with expression value above 0, are depicted by the red line.

<!!! width-max !!!>
![](053-kras.png)

<!!! float-aside !!!> 
Gene sets are lists of genes associated with a specific biological function. Preloaded gene sets are available in Orange through the Gene Sets widget.

KRAS is a member of the RAS protein family. RAS proteins function as molecular switches for signaling pathways critical to several aspects of normal cell growth. They are mutated in a variety of human tumors. The set of all RAS genes forms a gene set. More generally, gene sets are lists of genes associated with a specific biological function and are widely used in studying expression data. We will compare how well other genes in the RAS pathway separate the survival curves of cohorts.

Pass the information from [Genes](https://orangedatamining.com/widget-catalog/bioinformatics/genes/) to the Gene Sets widget. This widget can filter out a specific gene set from our expression data. On the left, we can select the organism and the gene set database we are interested in. Homo sapiens is already correctly marked. The Ras pathway is available through the KEGG pathway database. We choose KEGG on the right and write ‘ras’ in the filter tab. The Ras signaling pathway contains 232 genes, but only 219 have been found in our METABRIC dataset. Click on the pathway to output the filtered genes and their expression values.

![](055-geneset.png)

Now, connect the output with [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/). Previously, we used this widget for ranking clinical features to figure out which ones best separate cohorts according to survival. This time, we will use it for ranking genes in a gene set! Because gene expression values are numeric, the [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/) widget forms cohorts by splitting the expression values at the median. Let’s order the genes according to the p-value. We find that KRAS is only in 33rd place! The gene that is best at separating patients by survival is FLT3. Select the gene by clicking on it. If we want to know what FLT3 means, we can pass the information to the [Genes](https://orangedatamining.com/widget-catalog/bioinformatics/genes/) widget. The protein product of FLT3 expression functions as a receptor tyrosine kinase that is normally expressed on hematopoietic stem cells. Its mutations are well studied in acute myeloid leukemia; however, upregulated FLT3 expression has also been observed in lymph node metastases of patients with primary breast cancer.

![](056-rank.png)

On the left, select FLT3, and on the right, choose to form intervals of equal frequency.

Let’s go ahead and plot the survival curves defined by FLT3. Pass the output from [Rank Survival Features](https://orangedatamining.com/widget-catalog/survival-analysis/rank-survival-features/) to [Discretize](https://orangedatamining.com/widget-catalog/transform/discretize/) and then to the [Kaplan-Meier Plot](https://orangedatamining.com/widget-catalog/survival-analysis/kaplan-meier-plot/). We group by FLT3 and select to display confidence intervals and the median.

![](058-kmplot.png)

We can now compare the two plots side by side, one grouping patients according to the expression of KRAS and the other according to the expression of FLT3. There is a visible difference! Notice that whereas above median expression of KRAS is predictive of poor survival, above median expression of FLT3 is predictive of higher survival probability. Indeed, a quick search through the literature confirms that higher expression of FLT3 indicated a favorable prognosis in patients with breast cancer.
