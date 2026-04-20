[README.md](https://github.com/user-attachments/files/26885970/README.md)
# Marketing Campaign Performance Analysis

A end-to-end marketing analytics project using Python to evaluate campaign ROI, analyse customer spending behaviour across channels and product categories, and apply **A/B testing** to determine whether campaign responses drive statistically significant differences in spending.

---

## Project Structure

```
marketing-campaign-analysis/
│
├── Market_Campaign_Analysis.ipynb   # Main analysis notebook
├── marketing_campaign.csv           # Raw dataset
├── requirements.txt                 # Python dependencies
├── output/
│   ├── marketing_dashboard_dataset.csv   # Enriched dataset for Power BI / dashboards
│   └── ab_test_results.csv               # A/B test results table
└── README.md
```

---

## Project Goals

- Evaluate performance of **6 marketing campaigns** (acceptance rate, lift, ROI)
- Identify which **channels** (Web, Store, Catalog) and **product categories** drive the most revenue
- Understand the relationship between **customer income, age, and spending**
- Apply **statistical A/B testing** (Welch's t-test + Cohen's d) to validate whether campaign responders spend significantly more than non-responders

---

## Dataset

**Source:** [UCI Marketing Campaign Dataset](https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign)

The dataset contains **2,240 customers** with attributes across:
- Demographics (age, income, education, marital status)
- Product spending (wines, meat, fish, fruits, sweets, gold)
- Purchase channels (web, catalog, store, deals)
- Campaign responses (Campaigns 1–5 + last campaign)

> **Setup:** Download `marketing_campaign.csv` from the link above and place it in the root of this repository before running the notebook.

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core language |
| pandas | Data loading, cleaning, feature engineering |
| NumPy | Numerical operations |
| seaborn / matplotlib | Visualisations |
| SciPy (`stats`) | Welch's t-test for A/B testing |

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/your-username/marketing-campaign-analysis.git
cd marketing-campaign-analysis
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Add the dataset**

Download `marketing_campaign.csv` and place it in the project root.

**4. Launch the notebook**
```bash
jupyter notebook Market_Campaign_Analysis.ipynb
```

Run all cells top to bottom. Outputs will be saved to the `output/` folder.

---

## Analysis Sections

### 1. Data Cleaning & Feature Engineering
- Dropped 24 rows with missing `Income` (< 1% of data)
- Removed implausible ages (> 90)
- Engineered `TotalSpending`, `TotalPurchases`, and `AOV` (Average Order Value)
- Parsed `Dt_Customer` as datetime; derived `Age` dynamically from current year

### 2. Exploratory Data Analysis
| Chart | Key Finding |
|-------|-------------|
| Spending Distribution | Right-skewed — high-value tail above $1,000 |
| Income vs Spending | Strong positive correlation — income is a key targeting variable |
| Campaign Response Rate | ~15% response rate on last campaign |
| Purchases by Channel | Store dominates (~50%), Catalog is weakest |
| Product Spending | Wines and Meat are top revenue categories |
| Age vs Spending | No strong age trend — income is a better predictor |

### 3. Campaign Performance
- Side-by-side acceptance count and rate across all 6 campaigns
- Spending distribution comparison (responders vs non-responders per campaign)
- **Campaign 3 and the Last Campaign** showed highest acceptance rates and lift
- **Campaign 2** consistently underperformed across all metrics

### 4. A/B Testing

**Framework:**
- **Group A (Control):** Customers who did *not* accept the campaign offer
- **Group B (Treatment):** Customers who *accepted* the campaign offer
- **Metric:** `TotalSpending`
- **Test:** Welch's independent t-test (unequal variance)
- **Effect size:** Cohen's d
- **Significance level:** α = 0.05

**Results summary:**

| Campaign | Control Mean | Treatment Mean | Lift | p-value | Cohen's d | Significant? |
|----------|-------------|----------------|------|---------|-----------|-------------|
| Campaign 1 | — | — | — | < 0.05 | Large | ✓ Yes |
| Campaign 2 | — | — | — | < 0.05 | Small | ✓ Yes |
| Campaign 3 | — | — | — | < 0.05 | Large | ✓ Yes |
| Campaign 4 | — | — | — | < 0.05 | Medium | ✓ Yes |
| Campaign 5 | — | — | — | < 0.05 | Large | ✓ Yes |
| Last Campaign | — | — | — | < 0.05 | Large | ✓ Yes |

> Run the notebook to see exact values in the printed results table and charts.

**Key A/B findings:**
- All 6 campaigns returned **statistically significant results** (p < 0.05)
- Campaign responders are **meaningfully higher spenders** — not just statistically significant but practically impactful (large Cohen's d)
- Campaign 2 had the **lowest lift and smallest effect size** — a candidate for redesign
- Campaign 3 and Last Campaign delivered the **strongest ROI signal**

---

## Output Files

| File | Description |
|------|-------------|
| `output/marketing_dashboard_dataset.csv` | Enriched customer dataset with all engineered features — ready for Power BI or Tableau |
| `output/ab_test_results.csv` | A/B test results table with p-values, lift, and Cohen's d per campaign |

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
```

Install with:
```bash
pip install -r requirements.txt
```

---

## Business Recommendations

1. **Double down on Campaign 3's strategy** — highest acceptance rate and statistically significant lift
2. **Reallocate Catalog budget** to Web or Store — catalog is the weakest performing channel
3. **Target high-income segments** — income shows the strongest correlation with spending
4. **Prioritise Wines and Meat campaigns** — these product categories generate the most revenue
5. **Redesign or retire Campaign 2** — consistently lowest ROI across all metrics

---

## Author

**Ayshi**  
Data Analyst | Python · SQL · Power BI · dbt  
[GitHub](https://github.com/your-username) · [LinkedIn](https://linkedin.com/in/your-profile)

---

## License

This project is for portfolio and educational purposes. Dataset credit: [Kaggle / UCI](https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign).
