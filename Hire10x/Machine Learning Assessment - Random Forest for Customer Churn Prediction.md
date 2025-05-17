## Background

You are tasked with developing a machine learning solution for a telecommunications company that wants to predict customer churn. This is a critical business problem as acquiring new customers costs 5-25x more than retaining existing ones. Your goal is to create a robust Random Forest model that accurately predicts which customers are at risk of churning so the company can proactively implement retention strategies.

## Dataset

You will use the Telco Customer Churn dataset from Kaggle:  [Dataset](https://drive.google.com/file/d/102Aa6cUC3vp80-e9SrVs9kg5ut5do8QE/view?usp=sharing)

This dataset contains information about a telecommunications company's customers, including:

- Customer demographics (gender, age range, partners, dependents)
- Account information (tenure, contract type, payment method, paperless billing, monthly charges, total charges)
- Services signed up for (phone, multiple lines, internet, online security, online backup, device protection, tech support, streaming TV and movies)
- Churn status (whether the customer left the company or not)

The dataset has a moderate class imbalance with approximately 26.5% of customers having churned, reflecting real-world conditions that your model must address.

## Tasks

### Part 1: Exploratory Data Analysis (30%)

1. Perform comprehensive exploratory data analysis:
    - Handle missing values with appropriate techniques
    - Identify and handle outliers using robust statistical methods
    - Analyze feature distributions and perform necessary transformations
    - Implement feature engineering to create at least 3 new meaningful features
    - Conduct multicollinearity analysis and address it appropriately
    - Visualize key insights using advanced visualization techniques
    - Analyze class imbalance and propose approaches to address it

### Part 2: Random Forest Implementation (40%)

1. Implement a Random Forest classifier for customer churn prediction:
    - Apply appropriate preprocessing techniques for categorical and numerical features
    - Implement at least two different resampling techniques to address class imbalance (e.g., SMOTE, ADASYN)
    - Implement different feature selection methods and evaluate their impact
    - Develop an ensemble approach that combines multiple Random Forest models with different hyperparameters
    - Create custom feature importance visualization and interpretation
    - Implement a feature selection pipeline based on importance scores
    - Add methods to handle categorical variables effectively
    - Develop strategies to prevent overfitting
2. Perform hyperparameter tuning:
    - Implement a grid search with stratified k-fold cross-validation
    - Tune at least 7 different hyperparameters including:
        - n_estimators
        - max_depth
        - min_samples_split
        - min_samples_leaf
        - max_features
        - bootstrap
        - class_weight
    - Visualize hyperparameter importance and their impact on model performance
    - Document the reasoning behind hyperparameter selection

### Part 3: Model Evaluation and Interpretation (30%)

1. Evaluate model performance using:
    - Confusion matrix with proper visualization
    - Precision, recall, F1-score, and support
    - ROC curve and AUC score
    - Precision-Recall curve and AUC-PR score
    - Lift and gain charts
    - Calibration curves
    - Additional custom metrics relevant to the business problem
2. Implement a threshold optimization technique to maximize business value:
    - Define a custom business metric that accounts for the cost of false positives and false negatives
    - Optimize the classification threshold to maximize this business metric
    - Analyze how different thresholds impact business outcomes
3. Feature importance and model interpretation:
    - Compare different feature importance methods (MDI, permutation importance, etc.)
    - Create partial dependence plots for top features
    - Implement SHAP or LIME for local explanations of selected predictions
    - Analyze feature interactions and their impact on predictions
    - Provide actionable business insights based on model interpretation
4. Compare your Random Forest model with:
    - At least two other tree-based ensemble methods (XGBoost, LightGBM, etc.)
    - A deep learning approach
    - A simple baseline model (logistic regression)
    - Analyze trade-offs between model complexity, accuracy, and interpretability

## Deliverables

1. A well-documented Jupyter notebook (.ipynb) with:
    - Clear markdown explanations of your approach and reasoning
    - Commented code explaining complex implementations
    - Visualizations with proper labeling and interpretation
2. A summary section with:
    - Key findings from EDA
    - Model performance comparisons
    - Business recommendations based on model insights
    - Limitations of your approach and areas for improvement
    - Specific retention strategies for different customer segments based on your analysis

## Evaluation Criteria

1. Code quality and organization
2. Depth and quality of EDA
3. Sophistication of Random Forest implementation and techniques
4. Thoroughness of model evaluation and interpretation
5. Business relevance of insights and recommendations

## Additional Guidelines

- Focus on practical implementation rather than theoretical explanations
- Include error handling in your code
- Optimize for both performance and interpretability
- Provide clear business recommendations based on your findings
