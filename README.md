# Exploratory Data Analysis — Retail Sales and Menu Nutrition

Two exploratory analyses built with pandas, seaborn and matplotlib: a year of
retail transactions, and the nutritional makeup of a fast-food menu. Both
datasets are included.

## Contents

| File | Dataset | What it explores |
|---|---|---|
| [`retail-sales-eda.html`](retail-sales-eda.html) | `retail_sales_dataset.csv` | 1,000 transactions over 2023 — who buys, what they buy, and how sales move month to month |
| [`menu-nutrition-eda.html`](menu-nutrition-eda.html) | `menu.csv` | 260 menu items across 9 categories — calories, macronutrients, and how they correlate |
| `EDA on retail.docx` | — | Written report |

> Both analyses survive as HTML exports; the source `.ipynb` files were lost.
> All code and output remain readable, but they can't be re-executed as-is.
> The CSVs are included so the work can be rebuilt.

---

## Retail sales

**`retail_sales_dataset.csv`** — 1,000 transactions from 2023-01-01 to
2024-01-01, spanning Beauty, Clothing and Electronics.

| Column | |
|---|---|
| `Transaction ID`, `Date`, `Customer ID` | transaction identity |
| `Gender`, `Age` | customer |
| `Product Category`, `Quantity`, `Price per Unit`, `Total Amount` | purchase |

**What the analysis does**

1. Removes duplicates, parses `Date` to datetime, and sets it as the index —
   which is what makes the time-series step possible.
2. **Customer profile** — age distribution as a 20-bin histogram with a KDE
   overlay, and a gender count plot.
3. **Purchase behaviour** — order totals by distribution, and product categories
   ranked by frequency using a horizontal count plot ordered by value counts.
4. **Spend by gender** — a bar plot summing `Total Amount` rather than averaging
   it, so it reads as total revenue contribution.
5. **Monthly trend** — `resample('M').sum()` on the datetime index to plot total
   sales per month across the year.
6. **Correlation matrix** — an annotated `coolwarm` heatmap over the numeric
   columns.

---

## Menu nutrition

**`menu.csv`** — 260 items across 24 nutritional columns, in 9 categories:
Breakfast, Beef & Pork, Chicken & Fish, Salads, Snacks & Sides, Desserts,
Beverages, Coffee & Tea, Smoothies & Shakes. Calories run from 0 to 1,880.

**What the analysis does**

1. Confirms the dataset is complete — no nulls in any of the 24 columns — and
   drops duplicates.
2. Summarises with `describe()`.
3. Counts items per category.
4. Plots the calorie distribution across the menu.
5. Builds a correlation matrix over the nutritional factors, which is where the
   interesting structure is: fat, saturated fat and calories move together, and
   the daily-value percentage columns are near-perfectly correlated with the
   absolute amounts they're derived from.

---

## A note on the repository name

The repository is named for retail sales, but until now it contained only the
menu nutrition analysis — the file was called `EDA on retail sales data (1).html`
while the code inside reads `menu.csv`. The genuine retail sales analysis had
never been committed.

Both are now here under names that say what they are.

## Running it

The HTML exports open in any browser. To rebuild the analyses from the CSVs:

```bash
pip install pandas matplotlib seaborn jupyter
jupyter notebook
```

## Sources

Both are public datasets: the retail transactions are a synthetic sales dataset,
and the menu data is the McDonald's nutrition facts dataset published on Kaggle.
