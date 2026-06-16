# eBay Women's Perfume: Exploratory Data Analysis & Market Landscape 🧪📊

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Tools](https://img.shields.io/badge/Tools-Python%20%7C%20Pandas%20%7C%20Matplotlib%20%7C%20Seaborn-blue)
![Domain](https://img.shields.io/badge/Domain-E--Commerce%20%26%20Fragrance%20Market-purple)

---

## 📌 Business Overview & Problem Statement

The fragrance industry is growing rapidly, particularly through online marketplaces like eBay. Consumers have a wide range of choices across brand, type, size, and price category — yet not all products achieve high sales. Some become best-sellers while others underperform despite being on the same platform.

This project conducts an **Exploratory Data Analysis (EDA)** on a women's perfume dataset from eBay (2024) to understand what characteristics drive high sales and revenue — providing actionable insights for sellers, buyers, and marketplace analysts.

> **"What are the key product characteristics that drive high sales and revenue for women's perfumes on eBay marketplace?"**

> **Note:** This project is the continuation of the [Data Preprocessing Pipeline project](../ebay-perfume-preprocessing-pipeline). The cleaned dataset from that pipeline is used as the starting point for this analysis.

---

## 🗂️ Repository Structure

```
ebay-perfume-eda
│
├── README.md                                        # Main project documentation
├── data/
│   └── ebay_womens_perfume_clean.csv                # Cleaned dataset from preprocessing pipeline
├── notebook/
│   └── MiniProject2_Benedictus_Irvanda_Nugroho_EDA.ipynb  # Jupyter Notebook for EDA
├── output/
│   ├── viz_top_brands.png                           # Top 10 brands by total sold
│   ├── viz_price_vs_sold.png                        # Scatter plot price vs sold
│   ├── viz_revenue_by_price_category.png            # Revenue distribution by price category
│   ├── viz_revenue_by_type.png                      # Revenue by perfume type
│   ├── viz_size_distribution.png                    # Perfume size distribution
│   └── viz_correlation_matrix.png                   # Correlation heatmap
└── report/
    └── EDA_Benedictus_Irvanda_Nugroho.pdf           # Full presentation deck
```

---

## 💻 Tech Stack & Analysis Pipeline

All analysis was conducted using Python with the following libraries: **Pandas, NumPy, Matplotlib, Seaborn, and Scipy**.

### 1. Data Sampling & Validation

A **10% random sample** (100 data points) was drawn from the cleaned population (998 rows) to validate representativeness. Key statistical metrics — mean, median, and quartiles — between sample and population showed very close alignment, confirming the sample is unbiased and representative of the full dataset.

### 2. Normality Testing (Shapiro-Wilk)

All numeric columns were tested for normality using the Shapiro-Wilk test. All p-values came in well below 0.05, confirming **non-normal distribution** across all columns. As a result, **non-parametric statistical methods** (Kruskal-Wallis) were used for hypothesis testing instead of ANOVA.

### 3. Hypothesis Testing (Kruskal-Wallis)

To formally test whether price category has a significant effect on sales volume:

- **H₀:** No significant difference in sales volume across price categories
- **H₁:** Significant difference in sales volume exists across price categories
- **Result:** p-value < 0.05 → **H₀ rejected** — price category significantly affects sales volume, statistically confirming that Budget and Midrange products outperform premium segments.

### 4. Feature Engineering (Extended from Preprocessing)

| New Feature | Description |
|-------------|-------------|
| **`revenue`** | `price × sold` — total revenue per listing |
| **`size_ml`** | Extracted perfume size in milliliters from product title text |
| **`price_category`** | Categorized price tiers: Budget ($0–30), Midrange ($31–80), Prestige ($81–150), Luxury (>$150) |
| **`country` & `state`** | Extracted from unstructured `itemLocation` text column |

### 5. Categorical Encoding

| Column | Method | Reason |
|--------|--------|--------|
| `type`, `country` | One-Hot Encoding | Low cardinality — few unique categories |
| `brand` (211 unique) | Binary Encoding | High cardinality — prevents dataset from becoming too wide |
| `price_category` | Ordinal Encoding | Ordered categories (Budget < Midrange < Prestige < Luxury) |

---

## 🔍 Key Insights & Findings

### 1. 🏆 Top Brands by Sales Volume

Calvin Klein, Versace, and Dolce & Gabbana dominate the eBay perfume marketplace by total units sold. Their winning formula: pairing a popular perfume type (EDP or EDT) with Budget-to-Midrange pricing — maximizing volume through accessibility rather than exclusivity.

| Brand | Type | Price Category | Total Sold |
|-------|------|---------------|------------|
| Calvin Klein | Eau de Parfum | Budget | 36,874 |
| Versace | Eau de Toilette | Budget | 14,147 |
| Versace | Eau de Parfum | Midrange | 11,583 |
| Dolce & Gabbana | Eau de Toilette | Midrange | 11,013 |

### 2. 💸 Price vs Sales: Lower Price = Higher Volume

A **weak negative correlation (-0.18)** exists between price and units sold. Products in the Budget and Midrange tiers consistently outsell Prestige and Luxury items. The Kruskal-Wallis test statistically confirms this difference (p < 0.05).

> The eBay perfume market is not a luxury market. Budget and Midrange products account for **97%** of all product listings (461 Budget + 463 Midrange vs. 69 Prestige + 5 Luxury).

### 3. 🌸 Eau de Parfum Dominates Revenue

Eau de Parfum (EDP) is the undisputed leader — both in product count (731 listings) and total revenue ($8,636,304). Consumers on eBay clearly prioritize long-lasting fragrance over other types.

| Type | Total Revenue | Product Count |
|------|--------------|---------------|
| Eau de Parfum | $8,636,304 | 731 |
| Eau de Toilette | $4,771,154 | 194 |
| Cologne | $319,279 | 41 |
| Others | < $100K each | < 15 each |

### 4. 📦 The 100ml Sweet Spot

Products in the **~100ml size range** represent the overwhelming majority of best-sellers (299,846 total bottles sold). This size hits the balance between value for money and long-term usability. An interesting secondary finding: **5ml sample sizes** have meaningful sales (14,325 units), revealing a consumer segment that trial-purchases before committing to full bottles.

### 5. 📈 Strong Revenue-Sold Correlation (r = 0.92)

An extremely strong positive correlation exists between units sold and revenue — every incremental increase in sales volume directly translates into proportionally higher revenue. This confirms that **volume strategy outperforms margin strategy** in this marketplace context.

### 6. ⚠️ 24 Critical Stockout Risk Products

Identified 24 high-selling products (sold > 258 units, top 25%) with critically low remaining stock (≤ 5 units, bottom 25%) — including bestsellers from **Carolina Herrera**, **Viktor & Rolf**, and **Juliette Has A Gun**. These products are at immediate risk of stockout and revenue loss.

---

## 💡 Strategic Recommendations

**1. Prioritize the Winning Product Profile for New Listings**
Sellers entering the eBay perfume market should focus inventory on: **Eau de Parfum type · Budget–Midrange pricing · ~100ml standard size**. This profile aligns with the dominant consumer preference and drives the highest volume.

**2. Introduce Sample Sizes (5–10ml) as a Trial Strategy**
The existence of a trial-purchase segment opens an opportunity: sellers can convert hesitant buyers by offering affordable sample listings before they commit to full-bottle purchases — especially effective for Prestige or Luxury products that struggle on marketplace platforms.

**3. Immediate Restock of High-Risk Products**
Prioritize restocking the 24 identified critical products. Brands like Viktor & Rolf's Flowerbomb and Carolina Herrera's Good Girl have demonstrated proven demand — stockouts directly translate to lost revenue and reduced listing visibility.

**4. Rethink Premium Product Strategy on eBay**
Luxury and Prestige perfumes underperform on eBay because online shoppers can't test fragrances before buying. Sellers in these segments should consider using eBay primarily for **promotional exposure or clearance stock**, while positioning offline retail as the primary channel for high-margin luxury sales.

---

## 📂 Dataset Information

| Attribute | Detail |
|-----------|--------|
| **Dataset** | eBay Women's Perfume Sales (web-scraped) |
| **Source** | [Kaggle](https://www.kaggle.com/datasets/kanchana1990/perfume-e-commerce-dataset-2024) |
| **Year** | 2024 |
| **Rows (raw)** | 1,000 |
| **Rows (cleaned)** | 998 |
| **Columns (raw)** | 10 |
| **Columns (final)** | 10 (after feature engineering & encoding) |

---

## 👤 Author

**Benedictus Irvanda Nugroho**
Data Analytics Portfolio Project · 2026

Focused on transforming raw business data into actionable insights through systematic data cleaning, rigorous exploratory analysis, and business intelligence reporting.

* **LinkedIn:** [irvandanugroho](https://linkedin.com/in/irvandanugroho/)
* **GitHub:** [Irvanda08](https://github.com/Irvanda08)
* **Email:** irvandanugroho08@gmail.com

---

*This project was completed as part of a professional Data Analytics portfolio (2026).*
