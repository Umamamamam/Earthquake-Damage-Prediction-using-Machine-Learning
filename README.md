# Earthquake Damage Prediction using Machine Learning

## Overview

This project focuses on predicting the severity of building damage caused by the 2015 Gorkha Earthquake in Nepal. Using machine learning techniques and structural, geographical, and socio-economic features of buildings, the model classifies the level of damage into different categories.

The objective is to assist disaster management authorities, government agencies, and urban planners in identifying vulnerable structures and prioritizing relief and reconstruction efforts.

---

## Problem Statement

Earthquakes can cause varying levels of damage to buildings depending on their construction materials, design, location, and surrounding conditions. Accurately predicting damage severity helps emergency responders allocate resources effectively and reduce future risks.

The goal of this project is to build a machine learning model that predicts the **damage_grade** of a building based on its characteristics.

---

## Dataset Information

The dataset contains information about buildings affected by the Nepal earthquake, including:

* Structural characteristics
* Building age
* Foundation type
* Roof type
* Number of floors
* Geographic location
* Land conditions
* Construction materials
* Ownership details

### Target Variable

**damage_grade**

* Grade 1 → Low Damage
* Grade 2 → Moderate Damage
* Grade 3 → Severe Damage

---

## Project Workflow

### 1. Data Collection

* Imported earthquake damage dataset
* Inspected dataset structure
* Identified missing values

### 2. Exploratory Data Analysis (EDA)

* Distribution of target classes
* Correlation analysis
* Feature importance analysis
* Outlier detection
* Data visualization using histograms and boxplots

### 3. Data Preprocessing

* Missing value treatment
* Encoding categorical variables
* Feature scaling
* Handling class imbalance
* Feature engineering

### 4. Model Building

Implemented multiple machine learning algorithms:

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost
* Gradient Boosting

### 5. Model Evaluation

Performance metrics used:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-Learn
* XGBoost
* Jupyter Notebook

---

## Results

The XGBoost model achieved the best performance among all tested algorithms.

| Model               | Accuracy |
| ------------------- | -------- |
| Logistic Regression | XX%      |
| Decision Tree       | XX%      |
| Random Forest       | XX%      |
| XGBoost             | 71%      |

The model successfully identified damage severity patterns based on building and geographical characteristics.

---

## Key Insights

* Building age significantly impacts damage severity.
* Construction material is one of the strongest predictors.
* Buildings with weak foundations are more vulnerable.
* Geographic location influences earthquake impact.
* Structural design plays a critical role in earthquake resistance.

---

## Future Improvements

* Hyperparameter optimization using GridSearchCV.
* Advanced feature engineering.
* Ensemble learning techniques.
* Deep learning approaches.
* Deployment using Flask or Streamlit.
* Real-time earthquake damage prediction dashboard.

---

## Project Structure

```text
Earthquake-Damage-Prediction/
│
├── data/
│   ├── train.csv
│   └── test.csv
│
├── notebooks/
│   └── Earthquake_Damage_Prediction.ipynb
│
├── models/
│   └── trained_model.pkl
│
├── images/
│   └── visualizations
│
├── README.md
│
└── requirements.txt
```

---

## Business Impact

This solution can help:

* Government disaster response teams
* Urban planning departments
* Insurance companies
* Emergency management authorities
* NGOs involved in disaster recovery

By predicting building vulnerability before disasters occur, stakeholders can make informed decisions and reduce potential losses.

---

## Author

**Umamaheshwar Reddy**

B.Tech CSE (AI & ML)
Alliance University, Bengaluru

---

## License

This project is licensed under the MIT License.
