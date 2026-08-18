# Customer Churn Intelligence

## Predictive Modeling, Customer Segmentation, and Retention Analytics

This project analyzes customer churn among 10,000 bank customers using exploratory data analysis, supervised machine learning, decision-threshold analysis, and customer segmentation.

The goal is not only to predict which customers are likely to leave, but also to understand the customer characteristics associated with churn and identify segments that could be prioritized for retention efforts.

## Business Questions

The analysis focuses on four questions:

1. Which customer characteristics are associated with churn?
2. How accurately can machine learning models identify customers at risk of leaving?
3. How does changing the classification threshold affect the tradeoff between identifying churners and generating false alerts?
4. Can customer segmentation help identify groups where churn is disproportionately concentrated?

## Data

The dataset contains 10,000 bank customers.

Customer characteristics include:

- Credit score
- Geography
- Gender
- Age
- Tenure
- Account balance
- Number of products
- Credit card ownership
- Active membership status
- Estimated salary

The target variable is `Exited`, where 1 indicates that a customer exited the bank and 0 indicates that the customer remained.

The observed churn rate is 20.37%, with 2,037 customers exiting and 7,963 remaining.

## Exploratory Findings

Exploratory analysis revealed several notable patterns.

Customers who exited were older on average, at approximately 44.8 years compared with 37.4 years among customers who stayed.

Churn also varied substantially by geography. German customers had an observed churn rate of 32.4%, compared with 16.2% in France and 16.7% in Spain.

Inactive customers had a churn rate of 26.9%, compared with 14.3% among active customers.

Product ownership showed a strongly nonlinear pattern. Customers with two products had the lowest observed churn rate at 7.6%, while customers with one product had a 27.7% churn rate. Churn increased sharply among customers holding three or four products.

These relationships are descriptive and predictive. They should not be interpreted as causal effects.

## Machine Learning

Four classification models were evaluated:

- Logistic Regression
- Neural Network
- Random Forest
- Gradient Boosting

The data were divided into an 80% training sample and a 20% holdout test sample using stratification to preserve the churn distribution.

Categorical variables were one-hot encoded. Standardization was fitted only on the training data for models that required feature scaling.

Because only about 20% of customers churned, model evaluation emphasized minority-class performance rather than accuracy alone.

Metrics included:

- Precision
- Recall
- F1 score
- ROC-AUC
- PR-AUC

## Model Results

Gradient Boosting produced the strongest overall discrimination.

| Model | Accuracy | Churn Precision | Churn Recall | Churn F1 | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression | 0.808 | 0.59 | 0.19 | 0.28 | 0.775 | 0.479 |
| Neural Network | 0.861 | 0.75 | 0.47 | 0.58 | 0.863 | 0.702 |
| Random Forest | ~0.86 | 0.70 | 0.53 | 0.61 | 0.861 | 0.695 |
| Gradient Boosting | ~0.87 | 0.80 | 0.50 | 0.61 | 0.871 | 0.721 |

The nonlinear models substantially improved churn detection relative to the logistic regression baseline.

Gradient Boosting achieved a ROC-AUC of 0.871 and PR-AUC of 0.721.

## Threshold Analysis

The default probability threshold of 0.50 is not necessarily the best decision rule for a customer-retention program.

Lower thresholds identify more potential churners but also increase the number of customers incorrectly flagged as high risk.

The project therefore evaluates multiple probability thresholds to illustrate the tradeoff between:

- Precision
- Recall
- Customers targeted
- Churners identified
- Churners missed
- False alerts

The appropriate threshold ultimately depends on the cost of retention outreach relative to the cost of losing a customer.

## Important Predictors

Gradient Boosting identified the strongest predictive features as:

1. Age
2. Number of products
3. Active membership status
4. Account balance
5. German geography

Age accounted for approximately 39.4% of model feature importance, followed by number of products at 29.8%.

Feature importance measures predictive contribution and should not be interpreted as evidence that these characteristics cause churn.

## Customer Segmentation

K-Means clustering was used as an exploratory segmentation technique.

The churn outcome was excluded from cluster construction so that the segments were based on customer characteristics rather than known churn status.

Four interpretable customer segments were identified:

### Active High-Balance

2,876 customers  
13.04% observed churn rate

These customers maintain relatively high balances and are active members.

### Multi-Product Low-Balance

2,761 customers  
11.92% observed churn rate

This group has the lowest churn rate and holds more products on average.

### Inactive High-Balance

3,247 customers  
28.58% observed churn rate

These customers maintain relatively high balances but are inactive members.

### Older High-Risk

1,116 customers  
36.29% observed churn rate

This segment has the highest observed churn rate and an average age of approximately 60.

## Retention Insight

The Inactive High-Balance and Older High-Risk segments together represent approximately 43.6% of customers but account for approximately 65.4% of all observed churn.

This concentration suggests that retention programs could prioritize high-risk customer profiles rather than applying the same intervention to the entire customer base.

## Methodological Note

The K-Means silhouette scores were modest, indicating that the customer population does not separate into sharply defined natural clusters.

The four-cluster solution is therefore treated as an exploratory, business-oriented segmentation rather than evidence of four objectively distinct customer populations.

Cluster selection balanced statistical separation with interpretability.

## Key Takeaway

The project demonstrates how predictive modeling and customer segmentation can complement one another.

Gradient Boosting provided the strongest overall churn discrimination, while customer segmentation revealed that a disproportionate share of observed churn was concentrated in two customer groups.

Together, these methods provide a framework for identifying high-risk customers, prioritizing retention resources, and supporting data-informed customer strategy.

## Tools

- Python
- pandas
- NumPy
- scikit-learn
- Matplotlib
- Logistic Regression
- Neural Networks
- Random Forest
- Gradient Boosting
- K-Means Clustering

## Limitations

This analysis is predictive rather than causal.

Associations between customer characteristics and churn should not be interpreted as evidence that changing those characteristics would reduce churn.

The dataset also does not contain information about retention intervention costs, customer lifetime value, or previous retention campaigns. Those variables would be necessary to optimize retention decisions based on expected financial value.

## Future Extensions

Potential extensions include:

- SHAP-based model explanations
- Probability calibration
- Customer lifetime value integration
- Cost-sensitive threshold optimization
- Retention uplift modeling
- A/B testing of targeted retention interventions
- Interactive churn and segmentation dashboard
