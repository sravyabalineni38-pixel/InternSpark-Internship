Titanic Survival Prediction-Short report
1. Objective
The objective of this project is to predict passenger survival on the Titanic based on demographic and travel information. This is a classic supervised learning problem with an imbalanced target (~38% survival rate).

2. Data Preprocessing
Dataset: 891 passengers, 12 features
Preprocessing steps:

Feature selection: Pclass, Sex, Age, SibSp, Parch, Fare, Embarked

Engineered feature: FamilySize (SibSp + Parch + 1)

Missing values: Age (median: 28), Embarked (mode: 'S')

Categorical encoding: Sex (male=1, female=0), Embarked (0/1/2)

Train/test split: 80/20 with stratification

3. Algorithms Compared
Algorithm	Key Characteristics
Logistic Regression	Linear model, interpretable, requires feature scaling
Random Forest	Ensemble of 100 decision trees, captures non-linear patterns, handles unscaled features
4. Evaluation Metrics (Test Set)
Metric	Logistic Regression	Random Forest
Accuracy	0.8045	0.8156
Precision	0.7895	0.7907
Recall	0.6818	0.7273
F1-Score	0.7317	0.7576
ROC-AUC	0.8685	0.8713
CV Accuracy (5-fold)	0.8014 (±0.023)	0.8110 (±0.027)
5. Model Selection Rationale
Selected Model: Random Forest

Justification:

Higher recall (0.727 vs 0.682): Better at identifying actual survivors (fewer false negatives)

Higher F1-score (0.758 vs 0.732): Better balance of precision and recall

Slightly better ROC-AUC (0.871 vs 0.869): Better discrimination between classes

Consistent cross-validation: Mean CV accuracy 0.811 vs 0.801

No scaling required: Simpler preprocessing pipeline

Trade-offs: Random Forest is less interpretable than Logistic Regression but offers feature importance analysis.

6. Key Insights from Feature Importance (Random Forest)
Feature	Importance
Sex (female=0, male=1)	0.245
Fare	0.203
Age	0.159
Pclass	0.149
FamilySize	0.122
Interpretation: Gender is the strongest predictor (women had higher survival rates), followed by fare paid (wealthier passengers survived more) and age (children prioritized).

7. Conclusion
The Random Forest classifier outperforms Logistic Regression on this dataset, achieving 81.6% test accuracy and 0.871 ROC-AUC. The model effectively captures non-linear relationships in the data (e.g., "women and children first" policy interacting with passenger class). For production use, the model is stable as evidenced by consistent cross-validation scores (standard deviation < 0.03).

Limitations: The model may not generalize to modern evacuation scenarios as the Titanic had unique social dynamics (class-based lifeboat access). Future work could include more feature engineering (ticket grouping, cabin letter extraction) and hyperparameter tuning.

