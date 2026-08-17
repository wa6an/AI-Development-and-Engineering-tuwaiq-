
# Kickstarter Campaign Success Prediction

## Project Overview

A Machine Learning classification project focused on predicting whether a Kickstarter campaign will be successful or unsuccessful using information available at the time of launch.

The project compares multiple classification models, performs hyperparameter tuning, analyzes model generalization, applies unsupervised learning, and explores dimensionality reduction using PCA.

## Objective

The main objective is to build a model that can help assess the likelihood of Kickstarter campaign success before launch.

**Target variable:**

* `1` = Successful
* `0` = Failed

**Problem Type:** Binary Classification

## Dataset

The dataset contains completed Kickstarter campaigns.

Each row represents one campaign, with features related to:

* Campaign goal
* Category and subcategory
* Country
* Currency
* Campaign duration
* Launch date information

The target variable is `success`.

## Data Preparation

The following preprocessing steps were performed:

* Checked missing values
* Checked duplicate records
* Converted date columns to datetime
* Validated goals, campaign duration, dates, and target values
* Standardized categorical values
* Analyzed goal outliers
* Applied log transformation to the campaign goal
* Removed `campaign_id`
* Removed raw date columns
* Used One-Hot Encoding for categorical variables
* Applied StandardScaler to numerical features
* Used pipelines to prevent data leakage

The data was split using a stratified **60/20/20** approach:

* 60% Training
* 20% Validation
* 20% Testing

## Exploratory Data Analysis

Key findings from the analysis:

* Failed campaigns generally had higher funding goals.
* Success rates varied across campaign categories.
* Most campaigns lasted around one month.
* Campaign goals were highly right-skewed.
* No single numerical feature was sufficient to clearly separate successful and failed campaigns.
* Category and goal showed useful predictive signals.

## Machine Learning Models

Five classification models were trained and compared:

1. Logistic Regression
2. K-Nearest Neighbors (KNN)
3. Decision Tree
4. Random Forest
5. Gradient Boosting

### Validation Performance

| Model               | Validation F1 | Validation ROC-AUC |
| ------------------- | ------------: | -----------------: |
| Logistic Regression |         0.894 |              0.939 |
| Gradient Boosting   |         0.887 |              0.927 |
| Random Forest       |         0.844 |              0.916 |
| KNN                 |         0.816 |              0.848 |
| Decision Tree       |         0.787 |              0.771 |

Logistic Regression achieved the strongest overall validation performance and provided a strong balance between predictive performance, generalization, interpretability, and computational cost.

## Cross-Validation

Five-fold cross-validation was used to check model stability.

| Model               | Mean CV F1 |
| ------------------- | ---------: |
| Logistic Regression |      0.882 |
| Gradient Boosting   |      0.878 |
| Random Forest       |      0.858 |
| KNN                 |      0.825 |
| Decision Tree       |      0.794 |

The results showed that Logistic Regression remained highly competitive across different training folds.

## Hyperparameter Tuning

Hyperparameter experiments were performed for all major models.

Examples include:

* Logistic Regression: `C`
* KNN: `n_neighbors`
* Decision Tree: `min_samples_leaf`
* Random Forest: `max_depth`
* Gradient Boosting: `learning_rate`

Gradient Boosting achieved the highest tuned validation F1 of **0.899**, only slightly improving over the Logistic Regression baseline of **0.894**.

This showed that increasing model complexity did not necessarily lead to a meaningful improvement.

## Final Model

The final model selected was **Logistic Regression**.

The selection considered:

* Validation F1
* ROC-AUC
* Train-validation generalization gap
* Interpretability
* Computational cost
* Real-world suitability

### Final Test Results

| Metric    | Score |
| --------- | ----: |
| Accuracy  | 0.856 |
| Precision | 0.837 |
| Recall    | 0.938 |
| F1 Score  | 0.885 |
| ROC-AUC   | 0.930 |

The high recall indicates that the model was effective at identifying successful campaigns, while the overall F1 and ROC-AUC demonstrate strong classification performance.

## Error Analysis

The main findings from error analysis were:

* False positives can be costly because they classify unsuccessful campaigns as successful.
* Some misclassified campaigns have characteristics similar to the opposite class.
* Additional factors such as marketing performance, audience size, and creator history could help explain some prediction errors.

## Unsupervised Learning

K-Means clustering was applied without using the target variable.

The clustering features were:

* Log-transformed goal
* Campaign duration
* Launch year
* Launch month

Different values of K were evaluated using the Silhouette Score.

**Selected K:** 4

**K-Means Silhouette Score:** 0.243

The resulting clusters mainly represented different campaign profiles based on goal size and duration.

### Cluster Profiles

* Cluster 0: Higher goals and longer campaigns
* Cluster 1: Higher goals and shorter campaigns
* Cluster 2: Lower goals and shorter campaigns
* Cluster 3: Lower goals and longer campaigns

## PCA Analysis

Principal Component Analysis (PCA) was used to investigate dimensionality reduction.

* Original encoded features: **90**
* PCA components: **27**
* Variance preserved: **95.3%**

However, reducing the dimensions decreased validation F1:

* Without PCA: **0.894**
* With PCA: **0.804**

Therefore, PCA simplified the feature space but did not improve predictive performance.

## Key Insights

* Campaign goal and category were among the clearest predictive signals.
* Log transformation helped handle highly skewed goal values.
* Preventing data leakage was an important part of the project.
* Logistic Regression provided strong performance with high interpretability.
* Gradient Boosting achieved the highest tuned validation F1, but the improvement was very small.
* More complex models did not always outperform the simpler baseline.
* Campaign profiles could be grouped into four clusters based mainly on goal and duration.
* PCA reduced dimensionality but negatively affected classification performance.

## Limitations

The dataset did not include some potentially important real-world factors, such as:

* Marketing activity
* Audience size
* Creator history
* External promotion
* Social media engagement

These missing variables may explain some of the model's errors.

## Recommendations

Future improvements could include:

* Adding creator history features
* Including marketing and audience-related features
* Testing additional ensemble models
* Performing more extensive feature engineering
* Exploring probability thresholds based on business requirements

The model should be used as an **early screening and decision-support tool**, rather than as a guarantee of campaign success.

## Tools & Technologies

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Machine Learning
* Classification
* K-Means Clustering
* Gaussian Mixture Models
* PCA
* Data Analysis
* Exploratory Data Analysis

## Project Structure

```text
Project-01/
├── Kickstarter_ML_Capstone_Project_(7).ipynb
└── README.md
```

## Learning Outcomes

Through this project, I practiced:

* End-to-end Machine Learning workflow
* Data cleaning and preprocessing
* Exploratory Data Analysis
* Feature engineering
* Classification model development
* Model comparison and evaluation
* Hyperparameter tuning
* Cross-validation
* Overfitting and underfitting analysis
* Error analysis
* K-Means clustering
* PCA and dimensionality reduction
* Interpreting and communicating ML results
