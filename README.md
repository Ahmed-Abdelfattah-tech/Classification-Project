# Kaggle Tabular Classification Project

## 📌 Project Overview

This project focuses on solving a **binary classification problem** using an anonymized tabular dataset.

The dataset contains ten numerical features with anonymized names (`f01`–`f10`) and a binary target variable. Since the original meaning of the features is not provided, the project focuses on the **machine learning workflow and predictive performance** rather than domain-specific interpretation.

The project covers the complete workflow from exploratory data analysis and preprocessing to model comparison, evaluation, feature importance analysis, and Kaggle submission.

The final CatBoost submission achieved a **ROC-AUC score of 0.86517 on the Kaggle public leaderboard**.

---

## 🎯 Objective

The main objective is to build a classification model that can effectively distinguish between the two target classes and generate probability predictions for unseen test data.

The primary evaluation metric is **ROC-AUC**, making probability-based predictions particularly important for evaluating model performance.

---

## 📊 Dataset

The dataset consists of a training set and an unseen test set.

| Dataset  |            Shape | Description                   |
| -------- | ---------------: | ----------------------------- |
| Training | `(103,217 , 12)` | 10 features + `id` + `target` |
| Test     |  `(44,236 , 11)` | 10 features + `id`            |

### Features

The available predictive features are:

```text
f01, f02, f03, f04, f05,
f06, f07, f08, f09, f10
```

The `id` column is used only as an identifier and was excluded from model training.

> **Note:** The feature names are anonymized, so their real-world meanings are not available. Therefore, feature importance is interpreted only in terms of predictive contribution.

---

## 🔎 Exploratory Data Analysis

The exploratory analysis included:

- Dataset dimensions
- Data types
- Summary statistics
- Missing-value analysis
- Duplicate-value checking
- Target distribution
- Feature distributions
- Feature relationships

### Missing Values

Missing values were found in two features:

| Feature | Missing Values |
| ------- | -------------: |
| `f04`   |         20,118 |
| `f06`   |          2,634 |

The missing values were handled using **median imputation**.

The test set also contained missing values in the same features.

---

## ⚖️ Target Distribution

The target variable is imbalanced.

The positive class represents approximately **6.69%** of the training data.

Because of this imbalance, accuracy alone would not be an appropriate metric for comparing the models.

The project therefore uses **ROC-AUC** as the main evaluation metric.

---

## ⚙️ Data Preprocessing

The preprocessing workflow included:

1. Loading the training and test datasets.
2. Inspecting the dataset structure and data types.
3. Identifying missing values.
4. Handling missing values using median imputation.
5. Removing the `id` column from the model features.
6. Separating features and target.
7. Splitting the training data into training and validation sets.
8. Using a **stratified split** to preserve the target distribution.
9. Evaluating model predictions using ROC-AUC.

The validation split used:

```python
test_size=0.2
random_state=42
stratify=y
```

---

## 🤖 Models

A baseline model was first established using **Logistic Regression**, followed by several tree-based ensemble and boosting models.

### Baseline

- Logistic Regression

### Ensemble & Boosting Models

- Random Forest
- XGBoost
- LightGBM
- CatBoost
- Gradient Boosting
- HistGradientBoosting

This progression provides a comparison between a simple linear baseline and more powerful nonlinear ensemble methods.

---

## 📈 Model Performance

All models were evaluated using **Validation ROC-AUC**.

| Model                | Validation ROC-AUC |
| -------------------- | -----------------: |
| Logistic Regression  |        **0.69232** |
| Random Forest        |        **0.86631** |
| CatBoost             |        **0.86621** |
| LightGBM             |        **0.86526** |
| XGBoost              |        **0.86508** |
| HistGradientBoosting |        **0.86467** |
| Gradient Boosting    |        **0.86367** |

### Performance Comparison

The results show a substantial improvement from the Logistic Regression baseline to the ensemble-based models.

- Logistic Regression: **0.69232**
- Best validation result: **Random Forest — 0.86631**

This indicates that the relationship between the anonymized features and the target is likely more effectively captured by nonlinear ensemble models than by a simple linear classifier.

---

## 🏆 Final Model

Although Random Forest achieved the highest validation ROC-AUC (**0.86631**), **CatBoost** was selected for generating the final Kaggle submission.

CatBoost validation performance:

**ROC-AUC: 0.86621**

The final predictions were generated as probabilities for the positive class.

---

## 🥇 Kaggle Result

The final CatBoost predictions were saved to:

```text
Cat_Submission.csv
```

The submission achieved the following public leaderboard result:

### **Kaggle Public Leaderboard ROC-AUC: 0.86517**

The local CatBoost validation score was **0.86621**, while the Kaggle public leaderboard score was **0.86517**.

The close scores indicate that the model achieved similar performance on the unseen Kaggle evaluation data.

---

## 🔍 Feature Importance

Feature importance was analyzed using the Random Forest model.

The analysis identifies which anonymized features contributed most strongly to the model's predictive decisions.

The feature importance analysis is intentionally presented without assigning real-world meanings to the features because the dataset does not provide their descriptions.

### Most Important Features

The strongest contributors included:

- `f10`
- `f09`
- `f01`
- `f03`

while features such as `f06` and `f08` had relatively lower importance.

---

## 🧠 Key Machine Learning Concepts Demonstrated

This project demonstrates practical application of:

- Exploratory Data Analysis
- Missing-value handling
- Median imputation
- Class imbalance analysis
- Stratified train/validation splitting
- Binary classification
- Logistic Regression
- Random Forest
- Gradient Boosting
- XGBoost
- LightGBM
- CatBoost
- HistGradientBoosting
- Hyperparameter tuning
- Probability-based predictions
- ROC-AUC evaluation
- Feature importance analysis
- Kaggle submission workflow

---

## 🛠️ Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **XGBoost**
- **LightGBM**
- **CatBoost**
- **Joblib**
- **Jupyter Notebook**

---

## 📁 Project Structure

```text
Kaggle-Classification-Project/
│
├── Classification_Project.ipynb
├── Cat_Submission.csv
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone <repository-url>
cd Kaggle-Classification-Project
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Open the notebook

```text
Classification_Project.ipynb
```

Run the notebook cells sequentially to reproduce the analysis and model training workflow.

---

## 📌 Key Takeaways

This project demonstrates a complete practical machine learning workflow for an anonymized tabular classification problem.

Starting with **Logistic Regression as a baseline**, multiple ensemble and boosting algorithms were evaluated. The results showed that nonlinear ensemble models significantly outperformed the linear baseline.

The best local validation result was achieved by **Random Forest with a ROC-AUC of 0.86631**, while **CatBoost** was selected for the final Kaggle submission.

The final submission achieved:

> **0.86517 ROC-AUC on the Kaggle Public Leaderboard**

The project highlights the importance of model comparison, appropriate evaluation metrics, handling class imbalance, and validating models on unseen data.

---

## 👤 Author

**Ahmed Abdelfattah**

Aspiring **Applied AI / LLM Engineer**

Currently building practical experience across:

- Machine Learning
- Deep Learning
- NLP
- LLMs
- Applied AI
