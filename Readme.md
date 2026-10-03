# 🛒 Retail Store Sales – Exploratory Data Analysis

An exploratory data analysis (EDA) of 12,575 retail transactions (Jan 2022 – Jan 2025). The project cleans a dataset with missing values using the data's own rules, then explores what sells, when it sells and which categories drive revenue.

## Project Overview

| | |
|---|---|
| **Goal** | Clean the data accurately and uncover sales patterns across time and product categories |
| **Tools** | Python, pandas, NumPy, Matplotlib, Seaborn |
| **Notebook** | `RetailSalesEDA_.ipynb` |
| **Data period** | 1 Jan 2022 – 18 Jan 2025 |
| **Size** | 12,575 rows × 11 columns |

## Project Structure

```
Retail-Sales-Exploratory-Data-Analysis
│
├── data/
│   └── retail_store_sales.csv
│
├── RetailSalesEDA_.ipynb
│
└── README.md
```

## Dataset

| Column | Description |
|---|---|
| `Transaction ID` | Unique ID for each transaction |
| `Customer ID` | Customer identifier (only 25 unique values) |
| `Category` | Product category (8 categories) |
| `Item` | Item name; the suffix shows its category (e.g. `Item_10_PAT` = Patisserie) |
| `Price Per Unit` | Price of one unit (5 – 41) |
| `Quantity` | Units bought (1 – 10) |
| `Total Spent` | Price × Quantity |
| `Payment Method` | Cash, Credit Card or Digital Wallet |
| `Location` | Online or In-store |
| `Transaction Date` | Date of purchase |
| `Discount Applied` | True / False / missing |

## Data Cleaning Approach

Missing values: `Item` (1,213), `Price Per Unit` (609), `Quantity` (604), `Total Spent` (604) and `Discount Applied` (4,199).

Instead of filling with a mean or mode, the notebook first tests for hidden rules:

- `Total Spent = Price Per Unit × Quantity` in every complete row
- Each item has exactly **one** price
- A (Category, Price) pair identifies exactly **one** item

Using these rules:

1. **Price** is recovered from `Total ÷ Quantity`
2. **Item** is recovered from `Category + Price`
3. **Quantity** (604 rows that cannot be derived) is filled with the **median** and flagged in `Qty_imputed`
4. **Total Spent** is recalculated as Price × Quantity
5. **Discount Applied** is mapped to `Yes` / `No` / `Unknown`

Result: no missing values remain, and only 4.8% of rows rely on an estimate.

## Notebook Contents

1. Setup & Data Loading
2. Data Understanding (structure, duplicates, missing values, unique values)
3. Data Cleaning
4. Feature Engineering (year, quarter, month, day of week, weekend flag)
5. Outlier Detection & Treatment
6. Univariate Analysis (price, total spent, category distribution)
7. Time-Based Analysis (monthly, yearly, day of week, month × year heatmap)
8. Category Analysis
9. Key Findings & Recommendations

Every section ends with an **Insights** block explaining what the output shows.

## Key Findings

- **Total revenue** is about 1.64M. Yearly revenue was ≈ 540k (2022), ≈ 515k (2023) and ≈ 554k (2024). The changes follow transaction counts (4,134 → 3,987 → 4,241), not basket size.
- **January is the strongest month** in all three years (≈ 56k, 49k, 51k). Other months vary from year to year.
- **Friday is the best day** (≈ 245k) and **Monday the weakest** (≈ 223k), a gap of about 10%.
- **Spending per transaction is right-skewed**: median ≈ 110, mean ≈ 130.
- **Category revenue is very even**, so the ranking comes from basket size rather than footfall:

| Category | Revenue | Share |
|---|---|---|
| Butchers | ≈ 218k | 13.3% |
| Electric household essentials | ≈ 215k | 13.1% |
| Beverages | ≈ 207k | 12.6% |
| Furniture | ≈ 205k | 12.5% |
| Food | ≈ 205k | 12.5% |
| Computers and electric accessories | ≈ 202k | 12.3% |
| Patisserie | ≈ 195k | 11.9% |
| Milk Products | ≈ 190k | 11.6% |

## Recommendations

1. Prepare stock and staffing ahead of January, and run promotions in October and February.
2. Try a weekday offer to lift Monday sales.
3. Use bundles or upselling to raise Milk Products' basket value.
4. Record discount status for every sale so discount impact can be measured.


## ▶️ How to Run

### Option 1 – Google Colab
1. Go to [colab.research.google.com](https://colab.research.google.com) → **File → Upload notebook** and select `RetailSalesEDA_.ipynb`.
2. Upload `retail_store_sales.csv` using the **Files** panel (it must be in `/content/`).
3. Choose **Runtime → Run all**.

### Option 2 – Locally
```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook RetailSalesEDA_.ipynb
```
The notebook reads `/content/retail_store_sales.csv`. To run locally, change that path in the "reading the csv" cell to `retail_store_sales.csv`.

