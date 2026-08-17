# Kickstarter Campaign Success Prediction

A machine learning project that predicts whether a Kickstarter crowdfunding campaign is likely to succeed using information available at the time of launch.

## Project Overview

Kickstarter campaigns can have very different outcomes depending on factors such as funding goal, category, country, launch timing, and campaign duration.

The goal of this project is to build and compare machine learning models that can classify a campaign as:

* **1 — Successful**
* **0 — Failed**

The model is designed as an early screening tool to help understand campaign success patterns before launch.

## Dataset

The dataset contains **3,715 completed Kickstarter campaigns** with **13 features**.

Some of the main features include:

* Funding goal
* Country
* Currency
* Category
* Subcategory
* Campaign duration
* Launch year
* Launch month
* Launch weekday
* Campaign outcome

The target variable is `success`.

### Target Distribution

* Successful campaigns: **2,185**
* Failed campaigns: **1,530**

The classes are relatively balanced, with approximately **59% successful** and **41% failed** campaigns.

## Project Workflow

The project follows a complete machine learning workflow:

1. Problem and dataset understanding
2. Data quality assessment and cleaning
3. Exploratory Data Analysis
4. Feature preparation
5. Train, validation, and test splitting
6. Baseline model development
7. Multiple model training and comparison
8. Model evaluation
9. Overfitting and underfitting analysis
10. Hyperparameter experiments
11. Final model selection
12. Error analysis
13. Clustering
14. PCA dimensionality reduction
15. Final insights and recommendations

## Data Preparation

Several preprocessing steps were applied before model training.

* Converted date columns to the correct datetime format
* Checked missing values and duplicate rows
* Validated unrealistic or incorrect values
* Standardized categorical values
* Removed `campaign_id`
* Removed raw date columns
* Applied log transformation to highly skewed goal values
* Encoded categorical features
* Scaled numerical features when required
* Removed post-campaign information to prevent **data leakage**

Only information available at campaign launch was used for prediction.

## Exploratory Data Analysis

The analysis produced several useful findings:

* Failed campaigns generally had higher funding goals.
* Campaign success rates differed across categories.
* Most campaigns lasted around one month.
* Funding goals were highly right-skewed.
* No single feature was enough to completely separate successful and failed campaigns.

Overall, **goal and category were among the clearest signals related to campaign success**.

## Machine Learning Models

Five classification models were trained and compared:

* Logistic Regression
* K-Nearest Neighbors
* Decision Tree
* Random Forest
* Gradient Boosting

The models were evaluated using multiple metrics, including:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* Cross-validation F1

## Model Comparison

| Model               | Validation F1 | ROC-AUC |
| ------------------- | ------------: | ------: |
| Logistic Regression |         0.894 |   0.939 |
| Gradient Boosting   |         0.887 |   0.927 |
| Random Forest       |         0.844 |   0.916 |
| KNN                 |         0.816 |   0.848 |
| Decision Tree       |         0.787 |   0.771 |

Logistic Regression provided strong performance while maintaining a small train-validation gap.

## Hyperparameter Experiments

Hyperparameter experiments were performed for all main models.

The highest tuned validation F1 was achieved by **Gradient Boosting with a learning rate of 0.1**, reaching:

**Validation F1: 0.899**

However, this was only a small improvement over the Logistic Regression baseline of **0.894**.

The results showed that increasing model complexity does not always produce a meaningful improvement.

## Final Model

**Logistic Regression** was selected as the final model because it provided:

* Strong validation performance
* Good generalization
* High interpretability
* Low computational cost
* Performance close to more complex models

### Final Test Results

| Metric    |     Score |
| --------- | --------: |
| Accuracy  |     0.856 |
| Precision |     0.837 |
| Recall    |     0.938 |
| F1 Score  | **0.885** |
| ROC-AUC   | **0.930** |

The high recall indicates that the model was able to identify most successful campaigns.

## Error Analysis

The error analysis showed that:

* False positives are important because they may predict success for campaigns that actually fail.
* Some misclassified campaigns have characteristics very similar to the opposite class.
* Important external factors such as marketing, audience size, and creator history were not available in the dataset.

These missing variables may explain some of the remaining prediction errors.

## Clustering

Unsupervised learning was also explored to identify campaign profiles.

Clustering was based mainly on:

* Funding goal
* Campaign duration
* Launch year
* Launch month

The resulting clusters mainly represented different campaign profiles based on **goal and duration**, rather than directly separating successful and failed campaigns.

## PCA

Principal Component Analysis was tested to reduce the number of features.

PCA reduced:

**90 encoded features → 27 components**

while preserving:

**95.3% of the variance**

However, model performance decreased:

* F1 before PCA: **0.894**
* F1 after PCA: **0.804**

Therefore, PCA reduced dimensionality but did not improve prediction performance.

## Key Insights

* Funding goal and campaign category were important indicators of campaign success.
* Data leakage prevention was one of the most important steps in building a realistic model.
* More complex models did not automatically perform better.
* Logistic Regression achieved strong performance despite being relatively simple.
* PCA simplified the feature space but reduced predictive performance.
* Additional information about marketing, creator history, and audience size could improve future models.

## Tools and Libraries

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

## Files

* `Kickstarter_ML_Capstone_Project.ipynb` — Complete machine learning analysis and modeling
* `kickstarter_campaign_success.csv` — Dataset used in the project

## Dataset Source

Kickstarter Crowdfunding Success Analysis dataset.

## Conclusion

This project demonstrates a complete machine learning workflow, from data exploration and preprocessing to model comparison, tuning, evaluation, clustering, and dimensionality reduction.

The final Logistic Regression model achieved an **F1 score of 0.885** and a **ROC-AUC of 0.930** on the test set.

The model can be used as an early screening tool to support campaign evaluation, but it should not be treated as a guarantee of campaign success.
