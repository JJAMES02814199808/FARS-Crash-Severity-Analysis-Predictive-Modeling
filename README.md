# FARS 2020: Predicting and Analyzing Fatal Motor Vehicle Accident Severity

## 📊 Executive Summary
This project leverages the 2020 Fatality Analysis Reporting System (FARS) `accident.csv` dataset to uncover the primary behavioral and environmental drivers of fatal motor vehicle crashes in the United States. By curating a targeted feature set of fourteen core variables—including weather conditions, environments, human behavior, place, and date—this analysis delivers actionable insights to help policymakers and law enforcement design targeted interventions and improve road safety.

## 🔍 Data Engineering & The Data Leak Discovery
During the exploratory data analysis (EDA) and pipeline construction phase, a critical **data leak** was uncovered: initial predictive models exhibited artificially inflated performance due to the inclusion of the `FATALS` feature, which served as a direct proxy for our target variable (`SEVERITY`). 
* **Remediation:** The proxy feature was removed to ensure true out-of-sample predictive validity.
* **The Imbalance Challenge:** Removing the leak exposed a severe class imbalance in the dataset (~93% minor accidents vs. ~7% highly severe accidents). 

## 🤖 Machine Learning & The SVM vs. Random Forest Trade-Off
Faced with extreme class imbalance, standard baseline models failed to capture critical risk signals. 

* **The Baseline Failure:** A standard Random Forest Classifier completely missed severe cases, capturing a mere **2% recall** (detecting only 8 out of 506 actual severe crashes).
* **The SVM Solution:** A tuned Support Vector Machine (SVM) utilizing **balanced class weights** achieved a robust **61% recall** for severe crashes, successfully identifying **309 out of 506** actual severe cases (True Positives).

### The Public Safety Trade-Off
While the SVM dramatically improved sensitivity to the minority class, it introduced a necessary operational trade-off:
* **False Positives:** The model misclassified 3,793 minor accidents as severe.
* **Overall Accuracy:** Dropped to **44.01%**.
* **Domain Justification:** In public safety and emergency response analytics, **over-preparing for a potential hazard (a false positive) is significantly less costly than completely failing to identify a high-severity crash (a false negative).** 

## 📈 Visualizations & Confusion Matrix Analysis

```html](https://github.com/JJAMES02814199808/FARS-Crash-Severity-Analysis-Predictive-Modeling/blob/954089d826aa029f533c3bfc4578f48f1f46af69/confusion_matrix_retrained_svm.png)

