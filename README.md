# 🚗 Determinants of Vehicle Valuation in Sri Lanka's Online Secondary Market

> **An Analysis of the Pre and Early-2025 Import Liberalization Phases**  
> ST3011 Statistical Programming — Group 07 | Department of Statistics, Faculty of Science, University of Colombo

| Student ID | Name |
|------------|------|
| s16877 | D.A. Yahathugoda |
| s16798 | D.P. Haputhanthiri |
| s16810 | Ranindu Kariyapperuma |
| s16829 | Kavindu Perera |

---

> ⚠️ **Disclaimer:** This is a university learning exercise, not a production data science project. Methods were deliberately explored in depth — including parametric assumption testing, non-parametric alternatives, bootstrap analysis, and GAM modeling — for learning purposes.

---

## 📌 Overview

This study analyzes what drives used car prices in Sri Lanka's online secondary market during a period of extreme volatility — the **pre- and early-2025 import liberalization phase**. Using **9,676 listings** scraped from [Ikman.lk](https://ikman.lk) and [Riyasewana.lk](https://riyasewana.com), the analysis covers four key dimensions:

- Brand equity & depreciation
- Mechanical performance
- Comfort features
- Geo-economic market patterns

> **Context:** The 2020–2024 vehicle import ban created an abnormal market where used car prices kept rising with no ceiling. When the government announced the ban would be lifted in early 2025, the market froze — buyers stepped back expecting new imports, while sellers held onto their inflated prices. This study analyzes price behavior during this unusual period and the factors that drove it.

---

## 📂 Project Structure

```
├── ST3011_Group_Project.ipynb   # Main analysis notebook
├── requirements.txt             # Python dependencies
├── Project_Report.pdf           # Full project report
└── README.md
```

---

## 🗂️ Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | [Kaggle — Sri Lanka Used Car Market Dataset](https://www.kaggle.com/datasets/prasadnirmal/srilankan-second-vehiclecar-price-dataset) |
| **Original size** | 9,788 records, 16 variables |
| **After preprocessing** | 9,676 records, 15 variables (18 duplicates removed; "New" condition vehicles excluded) |
| **Target variable** | `price` (LKR Lakhs, log-transformed as `price_transformed`) |
| **Key features** | brand, model, YOM, engine capacity (cc), mileage, fuel type, gear type, comfort features (AC, power steering, power mirror, power window), town, leasing status |

The dataset is **downloaded automatically** via `kagglehub` when you run the notebook.

---

## 🎯 Objectives & Key Findings

### Objective 1 — Brand Equity and Depreciation Analysis

- **Toyota** serves as the mid-market benchmark for value retention in Sri Lanka
- **Tata** shows the steepest depreciation; **Mercedes-Benz** depreciates significantly with age
- Engine capacity has a moderate positive partial Spearman correlation with price (**ρ = 0.370**) after controlling for age and brand
- Age has a strong negative partial correlation (**ρ = −0.814**) — the primary depreciation driver
- GAM with smooth terms for age and log(engine_cc) used since OLS assumptions were violated

### Objective 2 — Mechanical Performance Analysis

- All four fuel types (Petrol, Diesel, Hybrid, Electric) differ significantly in median price (**Kruskal-Wallis H = 1606.22**)
- Alternative fuel vehicles (Hybrid + Electric) are priced significantly **higher** than traditional (Petrol + Diesel)
- **Automatic** cars are priced significantly higher than Manual (Mann-Whitney U, p ≈ 0)
- Engine segment significantly affects price, except Mid-range vs Large (no significant difference)

### Objective 3 — Comfort Feature Analysis

- **AC** has near-total market saturation (>95% of listings) — no longer a premium feature
- All four comfort features (AC, Power Steering, Power Mirror, Power Window) show statistically significant price premiums (Mann-Whitney U, p ≈ 0)
- Power Windows and Power Mirrors are strongly associated (**Cramér's V ≅ 0.63**) — typically bundled together

### Objective 4 — Market Sentiment and Geo-Economic Analysis

- **No statistically significant** price difference between Urban and Non-Urban listings (bootstrap 95% CI: −0.57, 3.95 — includes zero)
- **Leased vehicles** are priced significantly lower than non-leased (bootstrap 95% CI: −11.34, −3.75 — excludes zero)
- Western Province dominates listings; **Colombo** alone accounts for the largest share

---

## 📊 Final Model: GAM

| Metric | Value |
|--------|-------|
| **Pseudo R²** | 0.85 |
| **Significant predictors** | brand, age, engine capacity, gear, fuel type, leasing, AC, power steering |
| **Not significant** | province, power windows |

> Model adequacy checks were performed in R (code included in notebook as text cells) due to Python `pygam` limitations.

For full details, see [`Project_Report.pdf`](./Project_Report.pdf).

---

## ⚙️ How to Run

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Set Up Kaggle Credentials

The notebook downloads the dataset automatically via `kagglehub`.

- **Google Colab:** `kagglehub` will prompt you to authenticate interactively — no setup needed.
- **Local:** Place your `kaggle.json` in `~/.kaggle/kaggle.json` before running.

> Get your token from [kaggle.com](https://kaggle.com) → Account → Create New Token

### 3. Run the Notebook

```bash
jupyter notebook ST3011_Group_Project.ipynb
```

> **Note:** GAM model adequacy checks were performed in R. The relevant R code is included as text cells in the notebook for reference.

---

## 🛠️ Tech Stack

| Category | Libraries |
|----------|-----------|
| **Data** | `pandas`, `numpy`, `scipy` |
| **Modeling** | `pygam`, `scikit-learn` |
| **Statistics** | `statsmodels`, `pingouin`, `scikit-posthocs`, `diptest` |
| **Dimensionality Reduction** | `prince` (FAMD) |
| **Visualization** | `matplotlib`, `seaborn` |
| **Data Source** | `kagglehub` |

See [`requirements.txt`](./requirements.txt) for full details.

---

## 📄 License

This project is for academic purposes only.
