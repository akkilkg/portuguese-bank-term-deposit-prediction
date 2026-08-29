# Portuguese Bank Term Deposit Prediction

## 📌 Project Overview

This project analyzes the marketing campaign data of a Portuguese banking institution and develops machine-learning models to predict whether a customer is likely to subscribe to a term deposit.

The project combines exploratory data analysis, data preprocessing, classification modelling, hyperparameter tuning, probability-threshold optimization, and business recommendations to support more targeted bank marketing campaigns.

---

## 🎯 Business Problem

The bank conducts direct marketing campaigns to promote term deposits among existing customers.

The objective is to identify customers who are more likely to subscribe so that the marketing team can prioritize potential customers and improve campaign efficiency.

### Key Questions

- What customer and campaign characteristics are associated with term-deposit subscription?
- Which machine-learning model provides the strongest predictive performance?
- How can the model support customer targeting?
- What marketing strategies can improve campaign effectiveness?

---

## 📊 Dataset

The project uses the `bank-additional-full.csv` dataset from the Portuguese Bank Marketing dataset.

The dataset contains:

- **41,188 customer records**
- **21 variables**
- Customer demographic information
- Campaign/contact information
- Previous campaign outcomes
- Social and economic indicators
- Binary target variable: `y`

### Target Variable

`y`

- `yes` → Customer subscribed to a term deposit
- `no` → Customer did not subscribe

### Important Feature

The `duration` variable was excluded from the final predictive model because it represents the duration of the current call and is not available before the call takes place. Including it would introduce information leakage and would not represent a realistic pre-campaign prediction scenario.

---

## 🔍 Exploratory Data Analysis

The analysis covers:

- Dataset structure and data quality
- Missing and unknown values
- Duplicate records
- Target-class distribution
- Numerical variable distributions
- Categorical variable distributions
- Customer characteristics
- Campaign timing
- Previous campaign outcomes
- Economic indicators
- Bivariate relationships
- Multivariate relationships
- Outlier analysis

### Key EDA Insights

- The target variable is imbalanced, with non-subscribers representing the majority class.
- Previous campaign outcomes show a strong relationship with future subscription behaviour.
- Subscription rates vary across customer characteristics and campaign contact methods.
- Campaign timing and day of week show differences in subscription rates, although some differences are relatively small.
- Economic indicators provide additional context regarding the campaign environment.
- `pdays = 999` represents customers who were not previously contacted and therefore requires business-context interpretation.

---

## 🤖 Machine Learning

Four baseline classification models were developed:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. Gradient Boosting

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Because the target variable is imbalanced, model selection was not based on accuracy alone.

---

## 📈 Baseline Model Performance

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 83.50% | 36.79% | 64.66% | **46.89%** | 80.09% |
| Decision Tree | 82.08% | 34.66% | **66.70%** | 45.62% | 79.02% |
| Random Forest | 89.41% | 55.93% | 28.45% | 37.71% | 78.33% |
| Gradient Boosting | **90.11%** | **67.28%** | 23.71% | 35.06% | **80.91%** |

### Baseline Findings

- Logistic Regression achieved the highest F1-score.
- Decision Tree achieved the highest recall.
- Gradient Boosting achieved the highest accuracy, precision, and ROC-AUC.
- The different results demonstrate the trade-off between identifying more potential subscribers and reducing false-positive predictions.

---

## ⚙️ Hyperparameter Tuning

Gradient Boosting was selected for further optimization because of its strong baseline performance.

Hyperparameter tuning was performed using `RandomizedSearchCV` with ROC-AUC as the optimization metric.

### Tuned Gradient Boosting Performance

At the default probability threshold of 0.50:

| Metric | Score |
|---|---:|
| Accuracy | **90.34%** |
| Precision | **67.55%** |
| Recall | **27.37%** |
| F1-Score | **38.96%** |
| ROC-AUC | **81.40%** |

---

## 🎚️ Probability Threshold Optimization

The default classification threshold of 0.50 may not be optimal for an imbalanced marketing problem.

Probability thresholds were evaluated to examine the trade-off between:

- Precision
- Recall
- F1-score

The threshold producing the highest F1-score was selected as the operating point for the final evaluation.

A lower threshold can increase recall and allow the bank to identify more potential subscribers, although this can also increase false-positive predictions.

---

## 💡 Business Recommendations

### 1. Prioritize Customers with Successful Previous Campaign Outcomes

Customers with positive previous campaign outcomes should receive higher targeting priority because previous engagement provides useful information about future subscription propensity.

### 2. Use Predictive Customer Prioritization

The model can rank customers according to their predicted probability of subscribing, allowing the marketing team to focus resources on higher-probability customers.

### 3. Optimize the Classification Threshold

The bank should select the probability threshold according to the relative cost of missed opportunities and unnecessary marketing contacts.

### 4. Improve Contact Strategy

Differences in subscription rates across contact methods, months, and days of the week can support campaign scheduling decisions.

### 5. Use Customer Segmentation

Customer characteristics, campaign history, and economic indicators can be combined to create more targeted marketing segments.

### 6. Monitor Model Performance

The model should be periodically evaluated and retrained as new campaign data becomes available to account for changes in customer behaviour and economic conditions.

---

## ⚠️ Challenges Faced

### Class Imbalance

The positive class is substantially smaller than the negative class.

**Solution:** Multiple evaluation metrics including precision, recall, F1-score and ROC-AUC were used instead of relying solely on accuracy.

### Data Leakage

`duration` strongly relates to the target but is only known after the call.

**Solution:** The variable was excluded from the realistic predictive model.

### Unknown Values

Several categorical variables contain `unknown` values.

**Solution:** Unknown values were retained as a separate category and handled through categorical encoding.

### Outliers

Several numerical variables contain extreme observations.

**Solution:** Potential outliers were identified using the IQR method and evaluated using statistical and business context rather than automatically removing them.

### Categorical Variables

The dataset contains multiple categorical variables.

**Solution:** One-hot encoding was applied through a preprocessing pipeline.

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

---

## 📁 Project Structure

```text
Portuguese_Bank_Term_Deposit_Prediction/
│
├── README.md
├── Portuguese_Bank_Term_Deposit_Prediction.ipynb
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
└── images/
