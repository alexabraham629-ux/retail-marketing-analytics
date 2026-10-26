# Retail Marketing Analytics

Market Basket Analysis, internal sales-driver modelling and RFM customer segmentation on UK online-retail transactions, combined into one marketing strategy and a Python KPI dashboard.

**Author:** Alex Abraham · MBA (Business Analytics), CHRIST (Deemed to be University), Pune Lavasa Campus
**Course:** Marketing Analytics (MBA442B), CIA-4

---

## Business question

How can transaction-level retail data reveal **product affinities** (what sells together), **customer segments** (who to target) and **internal sales drivers** (when and under what conditions sales move), to guide cross-selling, bundling, retention and sales planning?

## What's inside

| Lens | Method | Headline result |
|---|---|---|
| Data preparation | UK filter, cancellation handling, non-product codes and duplicates removed; verified period 1 Dec 2010 – 9 Dec 2011 | 551,012 raw rows → 478,941 clean rows; £8.74M sales, 17,903 orders, AOV £488 |
| Market Basket Analysis | Apriori (mlxtend) on the top 120 products; min support 0.025, confidence ≥ 0.30, lift > 1 | 205 frequent itemsets, 154 rules; strongest rule lift 14.8 (Regency teacup and saucer set) |
| Sales-driver modelling | 54 weekly observations, chronological 43/11 split; Linear, Ridge, Lasso, Random Forest with TimeSeriesSplit tuning | Expanded linear model best: test RMSE £49,998, MAE £39,872, R² 0.15 (baseline R² −5.41); product breadth the largest positive driver |
| RFM segmentation | Quintile R/F/M scores + rule-based segments on 3,916 identifiable customers | Champions 857 (£4.56M, largest value), Loyal 698, Potential Loyalists 275, At Risk 594, Hibernating 972, Others 520 |
| Integration | Segment × product-affinity × sales-condition mapping | WHO (RFM) + WHAT (basket rules) + WHEN (sales drivers) strategy and KPI framework |
| Dashboard | Matplotlib / Seaborn / NetworkX notebook dashboard | KPI summary, rule network, segment profiles, scenario recalculation |

## Repository structure

```
retail-marketing-analytics/
├── notebooks/
│   └── marketing_analytics.ipynb   # Full analysis with outputs
├── data/
│   └── online_retail.xlsx          # Transaction workbook (sheet "Retail Dataset")
├── reports/
│   └── report.pdf                  # Full written report (59 pages)
├── requirements.txt
└── README.md
```

## Running it

```bash
pip install -r requirements.txt
jupyter notebook notebooks/marketing_analytics.ipynb
```

Run from the repository root so the notebook finds `data/online_retail.xlsx`, or edit `DATA_PATH` in the first code cell. The notebook uses only the first sheet and the period up to 9 December 2011.

## Limitations

- Association rules show co-occurrence, not causation.
- No channel-level advertising spend, so this is **internal** sales-driver modelling rather than spend-based MMM; coefficients are associations, not ROI.
- Only 54 weekly observations, so model estimates are noisy.
- RFM segments describe past behaviour; "At Risk" does not mean certain churn.

## Data source

Derived from the UCI Machine Learning Repository *Online Retail* dataset (Chen, D., 2015), licensed CC BY 4.0.

## Tech stack

Python (pandas, NumPy, mlxtend, scikit-learn, Matplotlib, Seaborn, NetworkX) · Jupyter
