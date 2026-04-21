# ML Assignment 1 — Regression on Gene Expression Data

## Overview
Regression analysis on transcriptomic data containing 5 genes across 3,000 
conditions. The goal is to model gene4's expression as a function of gene1, 
gene2, and gene3 using linear and polynomial regression with various 
regularization techniques.

**Course:** BINF 610 — Applied Machine Learning, University of Delaware

---

## Dataset
- Format: Tab-delimited transcriptomic data
- Size: 3,000 conditions (rows) × 5 genes (columns)
- Target variable: gene4
- Predictors: gene1, gene2, gene3
- Split: 2,500 training / 500 validation

---

## Models Implemented

### Part A — Linear Regression: g4 = a·g1 + b·g2 + c·g3 + d

|    Method           |     a |       b |        c |       d     | Train MSE | Val MSE |
|---------------------|--------|--------|--------|---------|-----------|---------|
| Closed-Form (Normal Eq.) | 1.7719 | 1.1235 | 0.8058 | 10.0141 | 0.02175 | 0.02254 |
| Gradient Descent (No Reg) | 1.7719 | 1.1235 | 0.8058 | 10.0141 | 0.02175 | 0.02254 |
| GD + Ridge (L2)     | 1.7650 | 1.1182 | 0.8018 | 10.0141 | 0.02177 | 0.02260 |
| GD + LASSO (L1)     | 1.7693 | 1.1215 | 0.8041 | 10.0141 | 0.02175 | 0.02256 |

### Part B — Polynomial Regression (Degree 3)
Features expanded: [g1, g1^2, g1^3, g2, g2^2, g2^3, g3, g3^2, g3^3]

| Method       | Train MSE  | Val MSE   |
|--------------|------------|-----------|
| Ridge (L2)   | 0.001064   | 0.000930  |
| LASSO (L1)   | 0.001055   | 0.000920  |
| Elastic Net  | 0.001055   | 0.000921  |

**Elastic Net Grid Search:** Best ratio = 1.0 (pure LASSO), 
searched from 0.0 to 1.0 with step 0.1


## Key Findings

### Underfitting vs Overfitting
- **Linear models → Underfitting:** Validation MSE stabilizes ~0.0225, 
  too high to capture the nonlinear gene relationships
- **Polynomial models → Good fit:** Validation MSE drops to ~0.00092, 
  with small train/val gap indicating good generalization

### Best Model
**Degree-3 Polynomial with LASSO regularization** is the best overall model:
- Validation MSE: 0.000920 (24x better than linear models)
- Stable learning curves with no significant overfitting
- Elastic net grid search confirms LASSO (ratio=1.0) as optimal

---

## How to Run
```bash
pip install numpy pandas matplotlib scikit-learn
python regression_assignment.py
```

---

## Files
- `regression_assignment.ipynb` — Full Python code
- `regression_writeup.pdf` — Detailed write-up with analysis
- `plots/` — All learning curve plots
- `data/` — Gene expression dataset (tab-delimited)
