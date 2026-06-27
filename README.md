# Earthquake Damage Prediction

## Overview

This project predicts the level of damage caused to buildings during the 2015 Gorkha earthquake in Nepal. The data comes from the "Richter's Predictor: Modeling Earthquake Damage" competition hosted by DrivenData, originally collected by Kathmandu Living Labs and the Central Bureau of Statistics, Nepal.

The goal is to predict `damage_grade`, which has 3 possible values:

- 1 = low damage
- 2 = medium damage
- 3 = almost complete destruction

## Folder Structure

```
project/
├── dataset/
│   ├── train_values.csv
│   └── train_labels.csv
├── notebook/
│   └── earthquake_prediction.ipynb
├── model/
│   └── xgboost_model.pkl
└── README.md
```

- `dataset/` — contains the raw input data (`train_values.csv`, `train_labels.csv`)
- `notebook/` — contains the main Jupyter notebook with all preprocessing, training, and evaluation steps
- `model/` — contains the final saved model (`xgboost_model.pkl`)

## Dataset

The dataset has 38 features describing each building, including:

- Location (geo_level_1_id, geo_level_2_id, geo_level_3_id)
- Structure details (count_floors_pre_eq, age, area_percentage, height_percentage)
- Construction type (foundation_type, roof_type, ground_floor_type, other_floor_type, plan_configuration)
- Superstructure material flags (mud, stone, brick, timber, bamboo, reinforced concrete, etc.)
- Ownership and usage details (legal_ownership_status, count_families, secondary use flags)

Categorical columns are obfuscated with random lowercase letters, so the same letter in different columns does not mean the same real-world value.

## Steps Followed

1. **Loaded and merged data**
   Combined `train_values.csv` and `train_labels.csv` using `building_id`, then dropped the ID column since it carries no predictive information.

2. **Outlier handling**
   Checked numerical columns using boxplots. Found outliers in several features. Used the IQR method with clipping (instead of removing rows) so no data was lost while reducing the effect of extreme values.

3. **Skewness check and fix**
   `age` and `area_percentage` were highly right-skewed. Applied `log1p` transformation to reduce skewness and make the distribution more balanced for training.
   `count_families` was left as is, since it only has 3 unique values and is a discrete feature, not a continuous one, so log transformation does not help here.

4. **Missing value check**
   Verified there were no missing values in the dataset, so no imputation was needed.

5. **Encoding categorical features**
   Applied One-Hot Encoding using `pd.get_dummies()` since models cannot work directly with text/category values.

6. **Train-test split**
   Split the data into training and testing sets (80/20) to evaluate the model on unseen data. A stratified split was used in later steps to keep the class proportions consistent, since `damage_grade` is imbalanced.

7. **Feature importance based selection**
   Trained an initial XGBoost model and checked feature importance. Removed features with very low importance (below 0.001) to reduce noise and dimensionality, then retrained the model on this smaller feature set.

8. **Hyperparameter tuning**
   Used `RandomizedSearchCV` to tune XGBoost hyperparameters (n_estimators, max_depth, learning_rate, subsample, colsample_bytree). Tuning gave little to no improvement over the original model, so the original XGBoost model was kept as final.

## Models Tried and Results

| Model | Weighted F1-Score |
|---|---|
| Logistic Regression | 0.53 |
| Decision Tree | 0.65 |
| Random Forest | 0.67 |
| Gradient Boosting | 0.71 |
| XGBoost | 0.73 |

XGBoost achieved the highest weighted F1-score and was selected as the final model.

## Why SVM and KNN Were Not Used

- **KNN** struggles when there are many columns (high dimensionality), which is the case here after one-hot encoding. Distance-based methods like KNN become unreliable in high dimensions, and KNN is also slow at prediction time with a large number of rows.
- **SVM** becomes very slow to train as the number of rows grows. With 260,000+ rows in this dataset, SVM training time becomes impractical.
- Tree-based and boosting models handle this kind of large, mixed categorical and numerical dataset much better, which is why they were the main focus of this project.

## Final Model

**XGBoost** was selected as the final model because it achieved the highest weighted F1-score among all models tested. The trained model is saved as `model/xgboost_model.pkl` using `pickle`.

## Challenges

- Large dataset increased training time.
- Hyperparameter tuning required additional computation.

## Future Improvements

- Try LightGBM.
- Explore additional feature engineering.
- Use cross-validation with more folds for further evaluation.

## How to Run

1. Place `train_values.csv` and `train_labels.csv` inside the `dataset/` folder.
2. Install required libraries:
   ```
   pip install pandas numpy scikit-learn seaborn matplotlib xgboost
   ```
3. Run the notebook `notebook/earthquake_prediction.ipynb` from top to bottom in order.
