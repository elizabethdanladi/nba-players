# Marketing Budget Allocation - Simple Linear Regression

## Project Overview
This project analyzes a marketing and sales dataset to identify which advertising channel (TV, Radio, or Social Media) has the strongest and most reliable relationship with Sales. A Simple Linear Regression model is fitted, validated, and used to produce a data-driven marketing budget recommendation.

## Repository Structure
- regression_analysis.ipynb — Main analysis notebook (all cells executed)
- marketing_and_sales_data_evaluate_lr.csv — Dataset
- README.md — This file

## Dataset
- File: marketing_and_sales_data_evaluate_lr.csv  
- Rows: 4,572 (4,546 after cleaning)  
- Columns:  
  - TV — TV advertising budget ($000s)  
  - Radio — Radio advertising budget ($000s)  
  - Social Media — Social Media advertising budget ($000s)  
  - Sales — Sales revenue ($000s)  

## Environment Setup
Install required packages with:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
## Key Results
| Metric              | Value                          |
|---------------------|--------------------------------|
| Selected Predictor  | TV                             |
| Model Equation      | Sales = 3.5615 × TV - 0.1325   |
| R²                  | 0.9990                         |
| Adjusted R²         | 0.9990                         |
| RMSE                | ~2.95                          |
| p-value (slope)     | < 0.0001                       |

### Assumption Tests
| Assumption       | Test                                | Result |
|------------------|-------------------------------------|--------|
| Linearity        | Corr(TV, residuals)                 | Met    |
| Normality        | Shapiro-Wilk (W = 0.9984, p = 0.94) | Met    |
| Homoscedasticity | Corr(fitted, \|residuals\|)         | Met    |
| Independence     | Durbin-Watson = 1.998               | Met    |

## Recommendation
Prioritize TV advertising as the primary marketing budget allocation.  
TV spend explains 99.9% of Sales variance — a uniquely strong and reliable predictor.  
For every additional $1,000 invested in TV, Sales increase by approximately $3,562.
