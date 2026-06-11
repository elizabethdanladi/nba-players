NBA Player Longevity Prediction

Naive Bayes Classification Project — Gaussian Naive Bayes Model

Project Overview:
This project analyses an engineered NBA player performance dataset (1,340 players, 10
features) using Python and Scikit-learn to build a Gaussian Naive Bayes classification
model that predicts whether a player will remain active in the NBA for at least 5 years
( target_5yrs ).
The analysis covers target variable confirmation, feature preprocessing for Gaussian
compatibility, train/test splitting, model training, Confusion Matrix evaluation, Precision and
Recall interpretation aligned with scouting priorities, a critical assessment of the Naive
Bayes independence assumption in a sports context, and actionable recommendations for
integrating the model into scouting workflows

Dataset:
Property Value
Source extracted_nba_players_data.csv
Rows 1,340 players
Features 10 continuous numeric metrics
Target Variable target_5yrs (1 = played 5+ years, 0 = did not)
Class Balance 62.0% career ≥5 yrs, 38.0% career <5 yrs
Missing Values None
The dataset is the engineered output from the NBA Feature Engineering pipeline — it
contains only continuous numeric features compatible with Gaussian Naive Bayes

Core Project Goals:
1. Load the engineered dataset and confirm target_5yrs as the classification target
2. Preprocess features to ensure compatibility with Gaussian Naive Bayes (continuous
metrics)
3. Split data into training and testing sets for unbiased model evaluation
4. Implement a Gaussian Naive Bayes classifier using Scikit-learn
5. Generate a Confusion Matrix to visualise true/false positives and negatives
6. Calculate Precision (minimise false positives: “busts”) and Recall (minimise false
negatives: missed talent)
7. Explain the Naive Bayes independence assumption and assess its realism for
basketball statistics
8. Summarise model reliability and limitations for a scouting department audience
9. Identify the most influential features driving longevity predictions
10. Provide actionable recommendations for integrating the model into scouting
workflows

Tools & Libraries
Tool Purpose
Python 3 Core language
pandas Data loading and manipulation
NumPy Numerical operations
scikit-learn GaussianNB model, train/test split, evaluation metrics
Matplotlib Data visualisation
Seaborn Correlation heatmap
Jupyter Notebook Interactive analysis environment

Modelling Approach
Algorithm: Gaussian Naive Bayes
Why Gaussian? All 10 features are continuous numeric metrics — Gaussian NB models
each feature as a normal distribution within each class
Why Naive Bayes? Computationally lightweight, probabilistic, interpretable, and
effective even on smaller datasets
No scaling required — Unlike Logistic Regression, GaussianNB models feature
distributions independently, so StandardScaler is not needed
Train / Test Split
80% training (1,072 players) / 20% testing (268 players)
random_state=42 for reproducibility

Results:
Performance Metrics
Metric Score
Accuracy 66.42%
Precision 86.92%
Recall 55.03%

Confusion Matrix:
Predicted: Did Not Last Predicted: Lasted 5+ Yrs
Actually Did Not Last 85 (TN) 14 (FP) — “Busts”
Actually Lasted 5+ Yrs 76 (FN) — Missed talent 93 (TP)

Business Interpretation (Scouting Context):
Precision (86.92%): When the model predicts a player will last 5+ years, it is correct
~87% of the time. This directly minimises wasted investment on busts — teams can
act on the model’s positive predictions with high confidence.
Recall (55.03%): The model only identifies ~55% of all truly long-term players, missing
76 genuine prospects. The model is conservative — it avoids false alarms but at the cost
of missing real talent.
For scouts: Use the model as a high-precision first-pass filter. Players flagged as longterm prospects should be fast-tracked. Players flagged negatively should still undergo
human evaluation — the model misses nearly half of real long-term players.

Key Findings:
Most Influential Features (Correlation with target_5yrs )
Rank Feature Correlation
1 total_points 0.3585
2 reb (rebounds) 0.2994
3 tov (turnovers) 0.2723
4 stl (steals) 0.2298
5 fg (field goal %) 0.2271
6 blk (blocks) 0.2101
7 efficiency 0.1945
8 ast (assists) 0.1754
9 ft (free throw %) 0.1067
10 3p (3-point %) ~0.000

Weakest predictor: 3p (three-point percentage) shows near-zero correlation with
longevity — shooting range alone does not predict career length.

Independence Assumption — Critical Assessment
Gaussian Naive Bayes assumes all features are conditionally independent given the class.
This assumption is violated in basketball data:
Feature Pair Why correlated
total_points ↔
reb , tov
High-usage players score, rebound, and turn the ball over more
efficiency ↔
most features
Engineered from pts + reb + ast + stl + blk − tov — shares
components with other columns
ast ↔ tov Both are ball-handling metrics that co-occur
Impact: The model double-counts correlated information, making it overconfident in its
probability estimates. However, classification accuracy is less sensitive to this than
probability calibration — the model’s 87% Precision confirms it still separates classes well
despite the violation.
Recommendation: Trust classification outputs; do not interpret raw probability scores as
precisely calibrated values.

Scouting Integration Recommendations
Model Output Trust Level Recommended Action
Predicts: Will last 5+ years High (87%
correct)
Prioritise for contract / development
investment
Predicts: Will NOT last 5+
years
Moderate (55%
recall)
Do not discard — assign for human
scout review
Borderline probability
(40–60%)
Low Mandatory human evaluation before any
decision.

Limitations & Next Steps
Low Recall (55%) limits the model’s usefulness for talent discovery — nearly half of
genuine long-term players are missed
Independence assumption violated — correlated features reduce the reliability of
probability outputs
No contextual features — position, team quality, age at entry, and injury history would
improve predictions
Threshold tuning — lowering the decision threshold from 0.5 to ~0.35 would improve
Recall at some cost to Precision
Next model comparison: Random Forest or Gradient Boosting are expected to
outperform Naive Bayes on this correlated dataset

Repository Structure:
- naive_bayes_nba.ipynb # Main analysis notebook (all cells executed)
-  extracted_nba_players_data.csv # Engineered dataset
- README.md # This file

  Project submitted as part of the Naive Bayes Mini Project — DH Foundation Data Science
Cohort

