# 🛒 Olist E-Commerce Analytics: End-to-End Data Project

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/Numpy-777BB4?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4CBA97?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

> **Author:** Mخhamed Gad 
> **Contact:** [LinkedIn](https://linkedin.com/in/muhamed-gad) | [GitHub](https://github.com/Muhamed-Gad)

---

## 📌 Project Overview
This project is an end-to-end data analytics solution using the **Olist Brazilian E-Commerce dataset**. It transforms raw, relational e-commerce data into actionable business intelligence. The project encompasses everything from initial data profiling and rigorous cleaning to advanced feature engineering, deep exploratory data analysis (EDA), and customer RFM (Recency, Frequency, Monetary) segmentation.

## ⚙️ How the Data Was Handled (Workflow)
The data processing pipeline was designed to be highly reproducible:
1. **Raw Data Extraction:** Imported multiple relational CSV files (Orders, Items, Customers, Sellers, Payments, Products).
2. **Data Quality & Schema Profiling:** Conducted thorough audits for missing values, invalid types, and business-logic contradictions (e.g., payment value vs. item total differences).
3. **Feature Engineering:** Calculated precise metrics such as `delivery_days`, `delivery_delay_days`, and created consolidated fact tables (`order_fact_clean`, `item_fact_clean`) to streamline the analysis.
4. **Metric Definitions:** Established strict business rules (e.g., *Merchandise value* excludes freight, while *Checkout value* includes freight; *Realized orders* only include 'delivered' statuses).
5. **Aggregation & Export:** Generated clean CSVs and analytical tables to be easily consumed by BI tools (like Power BI) or visualization libraries.

---

## 📓 Notebooks Breakdown
The core logic of the project is divided sequentially into 4 Jupyter Notebooks inside the `scripts/` directory:

* **`01_data_ingestion_and_profiling.ipynb`**  
  * Focuses on loading the raw datasets and generating a `raw_file_inventory`.
  * Performs initial schema profiling, data type checks, and missing value baselining to understand the raw data's health.

* **`02_cleaning_and_feature_engineering.ipynb`**  
  * The heaviest data processing phase. Handles missing values and data type conversions.
  * Calculates key delivery timelines (approval hours, delivery days, delays).
  * Merges multiple tables to create the central `order_fact` and resolves discrepancies (e.g., `payment_minus_item_total`, zero-value payment reviews).

* **`03_sales_and_operations_eda.ipynb`**  
  * Answers the core business questions. Analyzes monthly sales trends (orders and checkout values).
  * Evaluates top-performing product categories, sellers, and customer geographic states.
  * Assesses logistics performance (delivery days distribution) and customer payment behaviors (installments vs. payment types).

* **`04_customer_rfm_segmentation.ipynb`**  
  * Builds a robust Customer RFM Segmentation model.
  * Calculates Recency (days since last purchase), Frequency (total orders), and Monetary (total spend) for each `customer_unique_id`.
  * Assigns RFM scores and categorizes customers into actionable business segments (e.g., "Top Customers", "Recent One-time", "Churned").

---

## 📂 Project Structure
The repository strictly separates raw data, processed data, scripts, and outputs for maximum organization.

* **`scripts/`** - Python code and logic.
  * `01_data_ingestion_and_profiling.ipynb`
  * `02_cleaning_and_feature_engineering.ipynb`
  * `03_sales_and_operations_eda.ipynb`
  * `04_customer_rfm_segmentation.ipynb`
* **`raw_data/`** - Original Olist datasets (customers, orders, items, etc.).
* **`clean_data/`** - Processed datasets (`order_fact_clean`, `customer_rfm`, etc.).
* **`tables/`** - Aggregated CSV & Excel reports for BI tools.
* **`charts/`** - PNG visualizations generated during EDA.
* **`docs/`** - Documentation and final project reports (`final_project_report.md`).

---

## 📊 Key Findings & Results
Based on the analysis, several critical business insights were uncovered:
1. **Sales Seasonality & Trends:** A clear upward trend in monthly realized orders, with specific peaks indicating strong seasonality or marketing campaigns.
2. **Logistics Bottlenecks:** While the average delivery days are within acceptable ranges, the `delivery_days_distribution` highlights long-tail outliers (delayed deliveries) that negatively impact customer satisfaction, especially in remote states.
3. **Geographic Concentration:** The state of São Paulo (SP) dominates both as the primary origin of top sellers and the destination with the highest checkout volume.
4. **RFM Segments:** The customer base is heavily skewed towards one-time buyers. However, the top-tier RFM segments contribute a disproportionately large share of the total revenue, highlighting the need for targeted retention strategies.
5. **Payment Behavior:** Credit cards with high installment counts are the preferred payment method, strongly correlating with higher checkout values.

---

## 💡 Advice & Tips for Users
If you plan to fork, use, or review this repository, please keep the following in mind:
* **Path Management:** The project uses Python's `pathlib` for dynamic path resolution. Ensure you run the notebooks from within the `scripts/` directory or at the root level—the paths will adapt automatically.
* **Execution Order:** You **must** run the notebooks sequentially (`01` ➔ `02` ➔ `03` ➔ `04`), as subsequent notebooks depend on the `.csv` files generated in the `clean_data/` and `tables/` folders by the previous scripts.
* **Environment Setup:** It is recommended to create a virtual environment. You will need `pandas`, `matplotlib`, `seaborn`, and `jupyter`. 
* **BI Integration:** The outputs in the `tables/` and `clean_data/` directories are perfectly structured to be imported directly into Power BI or Tableau for interactive dashboarding.
