---
title: 'Quality Control and Data Preprocessing'
---

Study the following chapters to answer the quiz section below:

- <a href="/books/single-cell-tutorial-notes#Data-Preprocessing)" target="_blank">Chapter 4: Data Filtering and Preprocessing</a>


### Task 1 - Quality control 

Perform quality control on the expression matrix.

a) Discard genes that were not detected in at least 1% of all cells.

<Question
  id="sc-ex2-q1"
  points={1}
  type="multi"
  question="Which of the following is the correct filter setting for performing a)?"
  scorer={(answer) => answer === "b"}
  options={["A", "B", "C"]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">
  Since we want to filter out genes we have to set the Filter Type to Genes. Furthermore, we are interested only whether or not the gene was detected and not the quantity of the expressed gene, we choose to filter by Detection count.
  </Explanation>
</Question>

<!!! width-max !!!>
![](1abc_tile_annot.jpg)


<Question
  id="sc-ex2-q2"
  points={1}
  type="multi"
  question="What is the primary reason for filtering genes before further analysis?"
  scorer={(answer) => answer === "to remove genes that are never expressed or expressed in too few cells."}
  options={[
    "To remove uninformative genes that are never expressed or expressed in too few cells.",
    "To ensure that every gene is expressed in at least half of the cells.",
    "To reduce the number of samples in the dataset.",
    "To improve batch effect correction."
  ]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
</Question>


b) Filter cells based on a minimum number of 500 and a maximum number of 3000 expressed genes per cell.

<Question
  id="sc-ex2-q3"
  points={1}
  type="multi"
  question="Which of the following is the correct filter setting for performing b)?"
  scorer={(answer) => answer === "c"}
  options={["A", "B", "C"]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">
  Since we want to filter out cells we have to set the Filter Type to Cells. Furthermore, we are interested in the **number** of expressed genes per cell not in the total amount of transcripts per cell - so we again choose to filter by Detection count.
  </Explanation>
</Question>

<!!! width-max !!!>
![](2abc_tile_annot.jpg)


<Question
  id="sc-ex2-q4"
  points={1}
  type="multi"
  question="Why do we filter out cells with extremely high or low gene expression counts?"
  scorer={(answer) => answer === "All of the above."}
  options={[
    "Cells with very few detected genes may be damaged or of low quality.",
    "Cells with an unusually high number of expressed genes may be multiplets or artifacts.",
    "Removing extreme cells improves the accuracy of downstream clustering and visualization.",
    "All of the above."
  ]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
</Question>


c) Filter cells based on a minimum number of 6000 and a maximum number of 80000 transcripts per cell.

<Question
  id="sc-ex2-q5"
  points={1}
  type="multi"
  question="What do the points on the graph in the Filter widget represent in this third filtering step?"
  scorer={(answer) => answer === "cells"}
  options={["Genes", "Cells", "Transcripts"]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">
  Since we are again filtering out cells we have to set the Filter Type to Cells. This means that the points on the graph represent cells (the threshold marks which cells are going to be excluded from (or included in) further analysis).
  </Explanation>
</Question>



### Task 2 - Normalization and scaling

Normalize expression values for each gene in each cell to counts per 10000, logarithmize the values with natural logarithm and perform standardization with the Single Cell Preprocess widget.

<Question
  id="sc-ex2-q7"
  points={1}
  type="multi"
  question="Why do we need to normalize the gene expression values in single-cell analysis?"
  scorer={(answer) => answer === "to account for sequencing depth and make gene expression values comparable across cells"}
  options={["To eliminate biological variation between different cell types.", "To account for sequencing depth and make gene expression values comparable across cells.", "To change gene expression values so that all genes have the same expression level.", "Normalization is only needed for datasets with a small number of cells."]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">
  Raw gene expression values are influenced by technical factors such as sequencing depth. Normalization adjusts for these differences, allowing for meaningful comparisons of gene expression across cells.
  </Explanation>
</Question>


### Task 3 - Gene annotation

Map the genes in the dataset to the Entrez database.

<Question
  id="sc-ex2-q8"
  points={1}
  type="multi"
  question="How many genes were matched to the Entrez database?"
  scorer={(answer) => answer === "approximately 11000"}
  options={["Approximately 300", "Approximately 14000", "Approximately 11000"]}
  neutralOptions={["I don't understand the question."]}
  trials={2}
  timeout={10}>
  <Explanation after="correctOrMaxTrials">
  <!!! retina !!!>
  ![](sc-ex2-q8-exp.jpg)
  </Explanation>
</Question>


Plot the preprocessed and annotated data in a new t-SNE plot and compare it to the previous one. Quite the difference!







