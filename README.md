<div align="center">

# Fetal Health from Cardiotocography

**88.8% accuracy sounds good, until you see it misses more than 1 in 3 abnormal pregnancies**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)

</div>

> **TL;DR:** 2,126 cardiotocography (CTG) exams, which record fetal heart rate during pregnancy, are classified as *normal* or *abnormal* from 4 features. The random forest reaches **88.8% accuracy** against a 77.8% always-normal baseline, but catches only **63% of abnormal cases**. In screening, that recall on the minority class is the number that matters.

## Results

| Model | Accuracy | Normal correctly cleared | **Abnormal correctly flagged** |
|:--|--:|--:|--:|
| *Always predict "normal"* | *77.8%* | *100%* | *0%* |
| Gaussian Naive Bayes | 84.8% | 93.2% | 55.1% |
| Decision tree | – | 92.0% | **67.4%** |
| Random forest (N = 10 trees, depth 4) | **88.8%** | 96.3% | 62.7% |

The random forest settings came from a grid search over 1–10 trees and depth 1–5.

## What this shows

- **Class imbalance hides failure.** 78% of exams are normal, so a model can look strong while missing many abnormal cases.
- **The best model depends on the goal.** The random forest wins on accuracy, but the simpler decision tree catches the most abnormal cases.
- The same lesson drives my [cost-sensitive heart-disease project](https://github.com/Kunj2710/cvd-referral-cost-classifier): pick the metric that matches the real cost of a mistake.

## Data

[UCI Cardiotocography dataset](https://archive.ics.uci.edu/dataset/193/cardiotocography). NSP = 1 is treated as **Normal**; Suspect and Pathologic are merged into **Abnormal**. Save it as `cardiotocography_data_set.xls` next to the notebook.

```bash
pip install pandas numpy scikit-learn matplotlib seaborn xlrd
jupyter lab fetal_health_classification.ipynb
```

## What I'd do next

- Use **class weights or threshold tuning** to push abnormal recall above 90%, and report the false-alarm cost
- Use all 21 CTG features and keep **three classes** (Normal / Suspect / Pathologic)
- Report **precision–recall curves** instead of accuracy

<sub>Built during Boston University MET CS 577 (Data Science with Python), Spring 2026.</sub>
