# Skill Implementation Plan: data-science-patterns

## Overview
A comprehensive data science workflow skill providing structured EDA, feature engineering, model selection, and evaluation patterns for AI-assisted data science.

## Problem Statement
- Data scientists spend 60-80% of time on data preparation and EDA
- No standardized AI-assisted workflows exist
- Repetitive pattern recognition across projects
- Model selection often arbitrary or time-consuming
- Evaluation metrics selection confusing for beginners

## Target Market
- **Primary**: Data scientists, ML engineers
- **Secondary**: Data analysts, researchers
- **Tertiary**: Software engineers doing ML

## Success Metrics
- Complete EDA workflow coverage
- Feature engineering for all data types
- Model selection decision trees
- Proper evaluation framework
- Python code examples (pandas, sklearn, etc.)

---

## Implementation Checklist

### Phase 1: Core Skill Structure (Week 1)

#### 1.1 Create SKILL.md
```yaml
---
name: data-science-patterns
description: Structured data science workflows including EDA, feature engineering, model selection, and evaluation patterns with production-ready Python examples
tags: [data-science, machine-learning, pandas, sklearn, eda]
---
```

**Required Sections**:
- `# When to Use` - Trigger conditions
- `# Data Science Workflow` - End-to-end process
- `# EDA Patterns` - Exploratory data analysis
- `# Feature Engineering` - All data types
- `# Model Selection` - Decision trees
- `# Evaluation` - Metrics and validation

#### 1.2 Data Types Reference
Create `data-types-guide.md`:
- Numerical (continuous, discrete)
- Categorical (nominal, ordinal)
- Text data
- DateTime
- Image data
- Time series
- Geospatial

### Phase 2: EDA Workflows (Week 2)

#### 2.1 Structured EDA Guide
`eda-workflows/structured-eda.md`:
- Data loading and initial inspection
- Data profiling (pandas-profiling, ydata-profiling)
- Missing data analysis patterns
- Distribution analysis
- Outlier detection methods
- Correlation analysis
- Target variable analysis

#### 2.2 Missing Data Analysis
`eda-workflows/missing-data-analysis.md`:
- Missing data patterns (MCAR, MAR, MNAR)
- Detection methods
- Imputation strategies
- Deletion strategies
- Code examples for each approach

#### 2.3 Outlier Detection
`eda-workflows/outlier-detection.md`:
- Statistical methods (Z-score, IQR)
- Distance-based methods
- Isolation Forest
- Local Outlier Factor
- Domain-specific outlier handling

### Phase 3: Feature Engineering (Week 3)

#### 3.1 Numerical Features
`feature-engineering/numerical-features.md`:
- Scaling (StandardScaler, MinMaxScaler, RobustScaler)
- Transformations (log, sqrt, Box-Cox)
- Binning strategies
- Mathematical combinations
- Polynomial features

#### 3.2 Categorical Features
`feature-engineering/categorical-features.md`:
- One-hot encoding
- Label encoding
- Ordinal encoding
- Target encoding
- Binary encoding
- Hash encoding
- High cardinality handling

#### 3.3 Text Features
`feature-engineering/text-features.md`:
- TF-IDF
- Bag of Words
- Word embeddings (Word2Vec, GloVe)
- Transformer embeddings (BERT)
- Text preprocessing pipelines

#### 3.4 DateTime Features
`feature-engineering/datetime-features.md`:
- Component extraction (day, month, year)
- Cyclical encoding
- Time since events
- Rolling windows
- Seasonality features

#### 3.5 Feature Selection
`feature-engineering/feature-selection.md`:
- Filter methods (correlation, chi-square)
- Wrapper methods (RFE, forward/backward)
- Embedded methods (LASSO, tree importance)
- Dimensionality reduction (PCA, t-SNE, UMAP)

### Phase 4: Model Selection (Week 4)

#### 4.1 Classification Guide
`model-selection/classification-guide.md`:
- Decision tree for algorithm selection
- Logistic Regression
- Random Forest
- XGBoost/LightGBM/CatBoost
- SVM
- Neural Networks
- Multi-class strategies

#### 4.2 Regression Guide
`model-selection/regression-guide.md`:
- Linear Regression
- Ridge/Lasso/ElasticNet
- Random Forest Regressor
- Gradient Boosting
- SVR
- Neural Networks
- Time series regression

#### 4.3 Clustering Guide
`model-selection/clustering-guide.md`:
- K-Means
- Hierarchical Clustering
- DBSCAN
- Gaussian Mixture Models
- Cluster evaluation metrics

#### 4.4 Time Series Guide
`model-selection/time-series-guide.md`:
- ARIMA/SARIMA
- Prophet
- LSTM/GRU
- XGBoost for time series
- Cross-validation for time series

### Phase 5: Evaluation & Pipelines (Week 5)

#### 5.1 Metrics Selection
`evaluation/metrics-selection.md`:
- Classification: accuracy, precision, recall, F1, ROC-AUC
- Regression: MSE, RMSE, MAE, R², MAPE
- Ranking: NDCG, MAP
- Custom metrics
- When to use which metric

#### 5.2 Cross-Validation
`evaluation/cross-validation.md`:
- K-fold CV
- Stratified K-fold
- Time series split
- Group K-fold
- Nested CV

#### 5.3 Hyperparameter Tuning
`evaluation/hyperparameter-tuning.md`:
- Grid Search
- Random Search
- Bayesian Optimization (Optuna)
- Early stopping
- Hyperparameter importance

#### 5.4 Model Interpretability
`evaluation/model-interpretability.md`:
- Feature importance
- SHAP values
- LIME
- Partial dependence plots
- Permutation importance

#### 5.5 Pipelines
`pipelines/sklearn-pipelines.md`:
- Pipeline construction
- ColumnTransformer
- Custom transformers
- Pipeline persistence
- Production deployment patterns

---

## File Structure

```
data-science-patterns/
├── README.md
├── SKILL.md
├── getting-started.md
│
├── eda-workflows/
│   ├── structured-eda.md
│   ├── missing-data-analysis.md
│   ├── outlier-detection.md
│   ├── correlation-analysis.md
│   └── target-analysis.md
│
├── feature-engineering/
│   ├── numerical-features.md
│   ├── categorical-features.md
│   ├── text-features.md
│   ├── datetime-features.md
│   ├── feature-selection.md
│   └── feature-engineering-pipeline.md
│
├── model-selection/
│   ├── decision-matrix.md
│   ├── classification-guide.md
│   ├── regression-guide.md
│   ├── clustering-guide.md
│   ├── time-series-guide.md
│   └── ensemble-methods.md
│
├── evaluation/
│   ├── metrics-selection.md
│   ├── cross-validation.md
│   ├── hyperparameter-tuning.md
│   ├── model-interpretability.md
│   └── model-comparison.md
│
├── pipelines/
│   ├── sklearn-pipelines.md
│   ├── preprocessing-patterns.md
│   ├── model-deployment.md
│   └── monitoring.md
│
├── code-examples/
│   ├── pandas-patterns.py
│   ├── numpy-patterns.py
│   ├── sklearn-patterns.py
│   ├── complete-workflow.ipynb
│   └── production-pipeline.py
│
├── datasets/
│   ├── sample-datasets.md
│   └── data-generation.md
│
└── resources/
    ├── cheatsheets/
    ├── books-courses.md
    └── tools-libraries.md
```

---

## Content Requirements

### SKILL.md Content Outline

```markdown
# Data Science Patterns

## When to Use
- Starting a new ML project
- Need EDA guidance
- Feature engineering decisions
- Model selection uncertainty
- Evaluation strategy questions

## Workflow Overview
1. Data Understanding
2. EDA & Data Quality
3. Feature Engineering
4. Model Selection
5. Training & Evaluation
6. Deployment

## Quick Decision Trees

### Which Model for Classification?
```
Small dataset (<1000):
  → Logistic Regression, SVM

Medium dataset (1K-100K):
  → Random Forest, XGBoost

Large dataset (>100K):
  → XGBoost, LightGBM, Neural Networks

Need interpretability:
  → Logistic Regression, Decision Trees

Text data:
  → Naive Bayes, Transformers
```

### Which Metric to Use?
```
Balanced classes:
  → Accuracy, F1

Imbalanced classes:
  → Precision, Recall, F1, ROC-AUC

Cost-sensitive:
  → Use business metric, custom loss

Ranking problems:
  → NDCG, MAP
```

## EDA Checklist
- [ ] Data shape and types
- [ ] Missing values analysis
- [ ] Distribution analysis
- [ ] Outlier detection
- [ ] Correlation analysis
- [ ] Target variable analysis

## Feature Engineering by Data Type
[Comprehensive guides for each type]

## Code Snippets
[Copy-paste ready Python code]
```

---

## Code Example Requirements

### Minimum 10 Complete Examples
1. Complete EDA workflow
2. Missing data handling
3. Feature engineering pipeline
4. Classification model selection
5. Regression model selection
6. Cross-validation setup
7. Hyperparameter tuning
8. Model evaluation
9. Model interpretability
10. Production deployment

### Code Quality Standards
- PEP 8 compliant
- Type hints where helpful
- Docstrings for functions
- Error handling
- Memory-efficient patterns

---

## Quality Standards

### Accuracy
- Scikit-learn best practices (2024)
- Modern library versions (pandas 2.x, sklearn 1.3+)
- Production-ready code patterns
- Statistical correctness

### Completeness
- Cover all major ML problem types
- Address data quality issues
- Include model interpretability
- Production deployment guidance

### Usability
- Clear explanations
- Copy-paste ready code
- Decision trees for choices
- Common pitfalls highlighted

---

## Testing Strategy

### Example Validation
- All code examples run successfully
- Results match expected outputs
- Edge cases handled
- Memory constraints considered

### Workflow Validation
- End-to-end project guidance works
- Decision trees are accurate
- Recommendations are appropriate

---

## Marketing Positioning

### Key Messages
1. "Production-ready data science workflows"
2. "From data to deployment"
3. "AI-assisted ML engineering"
4. "Skip the boilerplate, focus on insights"

### Differentiators
- Comprehensive coverage from EDA to deployment
- Production-focused code examples
- Modern library versions
- Decision trees for common choices

### Target Keywords
data science, machine learning, pandas, scikit-learn, EDA, feature engineering, model selection, ML pipeline

---

## Implementation Timeline

| Week | Deliverable |
|------|-------------|
| 1 | SKILL.md + Data types guide |
| 2 | EDA workflows complete |
| 3 | Feature engineering guides |
| 4 | Model selection guides |
| 5 | Evaluation + Pipelines |
| 6 | Code examples + QA |

---

## Success Criteria

- [ ] Repository public
- [ ] 50+ code examples
- [ ] 4+ ML problem types covered
- [ ] All major Python DS libraries
- [ ] Production deployment guidance
- [ ] Validated with real projects
- [ ] 100+ installs in first month
