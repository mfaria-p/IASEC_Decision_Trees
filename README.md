# Cost-Sensitive Decision Trees for Imbalanced Classification

## Project Overview

This project presents the implementation and evaluation of a cost-sensitive decision tree algorithm aimed at improving minority class detection in imbalanced binary classification problems. The work was developed within the scope of the **IACEC - Introduction to Algorithms for Classification and Clustering** course.

Standard decision tree algorithms tend to optimize overall accuracy, often neglecting minority classes when datasets are highly imbalanced. This project addresses that limitation by introducing **cost-sensitive modifications to the CART (Classification and Regression Trees) algorithm**.

---

## Problem Statement

In imbalanced datasets, conventional decision trees favor the majority class, leading to:

* Poor recall for minority classes
* Misleadingly high accuracy

To mitigate this issue, we modify the decision tree learning process so that **misclassification of minority instances is penalized more heavily**.

---

## Main Contributions

* **Custom Decision Tree Implementation**
  Built from scratch, without relying on `rpart` internal optimizations.

* **Cost-Sensitive Learning**

  * Modified Gini impurity using instance weights
  * Weighted voting at terminal nodes
  * Configurable cost weights based on dataset imbalance ratio

* **Comprehensive Evaluation**
  Tested on **14 real-world imbalanced datasets** from OpenML.

* **Performance Metrics**

  * Accuracy
  * Precision (minority class)
  * Recall (minority class)
  * F1-score (minority class)

---

## Repository Structure

```text
├── g04_iacec_project.Rmd      # Main R Markdown file (implementation + analysis)
├── README.md                 # Project documentation
└── datasets/                 # OpenML datasets (not included in repository)
    ├── 15/
    │   ├── dataset.arff
    │   ├── dataset.pq
    │   ├── description.xml
    │   ├── features.xml
    │   └── qualities.xml
    ├── 310/
    ├── 1049/
    └── ...
```

---

## Requirements

### R Packages

Install the required packages with:

```r
install.packages(c(
  "rpart",
  "rpart.plot",
  "caret",
  "OpenML",
  "farff",
  "ggplot2",
  "gridExtra",
  "dplyr"
))
```

---

## Dataset Structure

Each dataset directory must contain at least:

* `dataset.arff` – Dataset in ARFF format
* `description.xml` – Dataset metadata

Datasets should be downloaded manually from **OpenML** and placed in the `datasets/` directory.

---

## Datasets Used

The evaluation uses **14 imbalanced binary classification datasets** from OpenML:

|   ID | Description                        | Domain           |
| ---: | ---------------------------------- | ---------------- |
| 1049 | PC hardware specifications         | Computer Science |
| 1050 | Student performance (Portuguese)   | Education        |
| 1053 | Student performance (Mathematics)  | Education        |
| 1063 | Glass identification               | Chemistry        |
| 1067 | Heart disease prediction           | Healthcare       |
| 1068 | Metal vs Rock music classification | Audio            |
| 1461 | Bank marketing                     | Finance          |
| 1464 | Blood transfusion prediction       | Healthcare       |
| 1480 | Liver disease diagnosis            | Healthcare       |
| 1487 | Ozone level detection              | Environment      |
| 1489 | Phoneme classification             | Linguistics      |
| 1590 | Adult census income                | Economics        |
| 6332 | Cylinder bands                     | Manufacturing    |
|  310 | Mammography                        | Medical Imaging  |

---

## Usage

1. **Prepare the datasets**
   Download the datasets from OpenML and organize them inside the `datasets/` folder.

2. **Run the analysis**
   Open `g04_iacec_project.Rmd` in **RStudio** and knit the document to HTML.

---

## Algorithm Description

### Standard Decision Tree

The baseline model follows the CART framework:

* Gini impurity as the split criterion
* Recursive binary splitting
* Majority voting at leaf nodes

### Cost-Sensitive Modifications

* **Weighted Gini Index**
  Minority class instances contribute more to impurity calculations.

* **Case Weighting**
  Each minority instance receives:

  ```text
  weight = min(imbalance_ratio, 10)
  ```

* **Weighted Predictions**
  Leaf node predictions are based on the **sum of weights**, not raw counts.

---

## Experimental Results

### Key Findings

* **Average Recall Improvement:** +47.94%
* **Average F1-Score Improvement:** +31.85%
* **Trade-off:** Slight decrease in accuracy (−3.21%)
* **Consistency:** Recall improved in **100% of datasets**

### Performance Comparison

| Metric       | Standard Tree | Cost-Sensitive Tree | Improvement |
| ------------ | ------------- | ------------------- | ----------- |
| Avg Recall   | 43.38%        | 91.32%              | +47.94%     |
| Avg F1-Score | 50.72%        | 82.57%              | +31.85%     |
| Avg Accuracy | 85.04%        | 81.83%              | −3.21%      |

Detailed results and visualizations are available in `g04_iacec_project.Rmd`.

---

## Visual Analysis

The project automatically generates:

* Recall comparison across datasets
* F1-score comparison
* Recall improvement vs. imbalance ratio
* Overall performance bar charts

---

## Future Work

* Extend the approach to **multiclass classification**
* Combine cost-sensitive learning with **SMOTE or resampling techniques**
* Implement **adaptive cost-weighting strategies**
* Explore **ensemble methods** (Random Forests, Boosting)
* Test on additional datasets with varying imbalance ratios

---

## Authors

- [Mariana Pereira](https://github.com/mfaria-p)
- [Leonor Couto](https://github.com/Leonor2004)

---

## License

This project is intended for **educational purposes only** as part of university coursework.
