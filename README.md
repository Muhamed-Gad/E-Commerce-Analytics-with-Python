# Olist E-Commerce Analytics with Python

An end-to-end data analytics graduation project based on the Brazilian Olist e-commerce dataset.

The project uses Python only to move from raw relational data to data-quality validation, cleaning, transformation, exploratory data analysis, customer segmentation, and business recommendations.

## Business objectives

This analysis answers the following questions:

- What are the main sales and checkout-value trends?
- Which product categories, sellers, and customer regions contribute the most?
- How effective is delivery performance across customer states?
- Which payment methods and installment patterns are most common?
- How many customers purchase again?
- Which customer segments should be prioritised for retention and growth?

## Dataset

Source: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The dataset contains anonymised marketplace transactions from Brazil between 2016 and 2018.

Download the dataset manually, then place these six CSV files inside `data/raw/`:

```text
customers.csv
orders.csv
order_items.csv
order_payments.csv
products.csv
seller.csv
```

Raw and processed data are excluded from GitHub through `.gitignore`.

## Project structure

```text
e-commerce_project/
├── data/
│   ├── raw/                     # Local only; ignored by Git
│   └── processed/               # Generated locally; ignored by Git
├── notebooks/
│   ├── 01_data_ingestion_and_profiling.ipynb
│   ├── 02_cleaning_and_feature_engineering.ipynb
│   ├── 03_sales_and_operations_eda.ipynb
│   └── 04_customer_rfm_segmentation.ipynb
├── outputs/
│   ├── figures/
│   ├── tables/                  # Generated locally; ignored by Git
│   └── final_project_report.md
├── .gitignore
├── README.md
└── requirements.txt
```

## Installation and execution

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install -r requirements.txt
py -m ipykernel install --user --name olist-analytics --display-name "Python (olist-analytics)"
jupyter lab
```

Open and run the notebooks in this exact order:

1. `01_data_ingestion_and_profiling.ipynb`
2. `02_cleaning_and_feature_engineering.ipynb`
3. `03_sales_and_operations_eda.ipynb`
4. `04_customer_rfm_segmentation.ipynb`

## Key findings

- The dataset contains 99,441 orders; 96,478 were delivered.
- Delivered checkout value reached 15.42 million currency units.
- Average checkout value was 159.83.
- Freight represented approximately 14.3% of checkout value.
- Average delivery time was 12.56 days, with an 8% late-delivery rate.
- `beleza_saude`, `relogios_presentes`, and `cama_mesa_banho` were the top categories by delivered checkout value.
- About 97% of observed customers made only one delivered purchase.
- Improving second-purchase conversion is the largest identified customer-growth opportunity.
- Customer state `AL` requires delivery investigation because its late-delivery rate was 24%.

## Data-quality decisions

- No duplicate candidate keys or broken tested relationships were found.
- Zero-value payment records were retained because they were voucher or undefined payment records.
- Invalid delivery timelines were excluded only from delivery-duration KPIs, not from sales analysis.
- Checkout value (`item price + freight`) is used as the primary sales measure; payment value is analysed separately to avoid reconciliation distortions.

## Recommendations

- Target recent one-time customers with second-purchase campaigns.
- Retain potential and at-risk repeat customers through personalised offers.
- Investigate carrier, seller, and freight patterns affecting delivery performance in `AL`.
- Protect availability and delivery capacity for high-volume product categories.
- Maintain a separate payment-reconciliation view instead of using payment value as sales revenue.

## Tools

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Project report

See [the final project report](outputs/final_project_report.md) for methodology, results, limitations, and business recommendations.
