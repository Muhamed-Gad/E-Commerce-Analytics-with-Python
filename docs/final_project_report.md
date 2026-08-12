# Olist E-Commerce Analytics — Final Report

## 1. Executive summary

This project analysed anonymised Olist marketplace transactions using Python, from raw multi-table CSV files through data-quality validation, cleaning, feature engineering, exploratory analysis, and RFM customer segmentation.

The analysis covers **99,441 orders** in the source extract. Of these, **96,478** were delivered and form the realized-sales and delivery-performance scope.

The principal business finding is that Olist's observed customer base is dominated by one-time buyers: **90,557 of 93,358 unique customers (about 97%)** placed only one delivered order in the extract. Improving second-purchase conversion is therefore a more material growth lever than treating the current repeat-customer base as the main growth engine.

## 2. Data quality and analytical scope

The raw data contains six relational tables: customers, orders, order items, payments, products, and sellers.

- Candidate keys had **no duplicate rows** and no null key values.
- All tested customer, order, product, seller, and payment relationships had **zero orphan records**.
- Nine zero-value payment records were retained because they were voucher or `not_defined` records, not automatically invalid transactions.
- Eight delivered orders had invalid purchase-to-delivery chronology and were excluded only from delivery-duration metrics; they were not deleted from sales analysis.
- For 1,359 orders, carrier handoff precedes approval. This remains a source-system timing anomaly and is excluded from approval-to-carrier process-time KPIs.

### Definitions

- **Merchandise value:** item price excluding freight.
- **Checkout value:** item price plus freight; the primary realized-order value in this report.
- **Payment value:** payment-table amount; analysed separately because it can differ from checkout value.
- **Realized order:** an order with status `delivered`.

## 3. Headline KPIs

| KPI | Result |
|---|---:|
| Delivered orders | 96,478 |
| Merchandise value | 13,221,498.11 |
| Checkout value | 15,419,773.75 |
| Average checkout value | 159.83 |
| Freight value | 2,198,275.64 |
| Freight share of checkout value | 14.3% |
| Valid delivered timelines | 96,470 |
| Average delivery time | 12.56 days |
| Late-delivery rate | 8% |
| Unique customers | 93,358 |
| Repeat customers | 2,801 |
| Repeat-customer rate | about 3% |

Values are reported in the currency units stored in the source dataset.

## 4. Key findings

### Sales and product mix

The three leading categories by delivered checkout value are:

1. `beleza_saude` — 1,412,089.53
2. `relogios_presentes` — 1,264,333.12
3. `cama_mesa_banho` — 1,225,209.26

`cama_mesa_banho` sells the highest number of items among these leaders, while `relogios_presentes` has the highest average item price. This suggests different commercial roles: volume-driving categories should be managed for availability and fulfilment, while higher-ticket categories merit conversion and margin review.

### Delivery operations

Overall delivery performance is 12.56 days on average, with 8% of valid delivered orders arriving late.

Customer state **AL** is a clear operational priority: its average delivery time is **24.54 days** and its late-delivery rate is **24%**, compared with 12.56 days and 8% overall. This evidence supports investigating carrier coverage, seller allocation, and freight-service levels for this destination.

### Payment behavior

Credit cards appear in **74,304 delivered orders (77.02% of delivered orders)** and have an average 3.50 installments. `boleto` appears in 19.89% of delivered orders. Percentages are not mutually exclusive because an order may have multiple payment records or payment methods.

Payment amount should not replace checkout value in sales KPIs: 378 orders have a material payment-to-item-total difference, concentrated mainly in credit-card payments. The data does not identify the commercial reason for every difference, so no causal claim is made.

### Customer behavior

The corrected segments show a large second-purchase opportunity:

| Segment | Customers | Customer share | Observed checkout value |
|---|---:|---:|---:|
| New / recent one-time | 45,136 | 48.35% | 7,297,809.27 |
| Hibernating one-time | 45,421 | 48.65% | 7,257,777.02 |
| Potential repeat customers | 1,401 | 1.50% | 409,327.65 |
| At-risk repeat customers | 1,258 | 1.35% | 378,395.15 |
| Champions | 141 | 0.15% | 76,376.39 |

Potential-repeat and at-risk repeat customers each have substantially higher average observed checkout value than one-time customers. They are small but valuable groups for targeted retention efforts.

## 5. Recommendations

1. **Prioritise second-purchase conversion.** Trigger a post-delivery campaign for `New / recent one-time` customers—product recommendations, limited-time credit, or category-specific bundles. Measure conversion to a second delivered order.
2. **Protect repeat customers.** Offer cross-sell to `Potential repeat customers`, and re-engagement incentives to `At-risk repeat customers`. Avoid expensive individual treatment of the large hibernating one-time segment until campaign tests prove return.
3. **Investigate AL delivery performance first.** Break results down by carrier, seller state, product category, and freight value to identify whether the delay is driven by a particular route or fulfilment pattern.
4. **Manage top categories differently.** Protect stock and delivery capacity for high-volume `cama_mesa_banho`; review conversion, promotion, and freight burden for high-value `relogios_presentes` and `beleza_saude`.
5. **Keep sales and payment reporting separate.** Use checkout value for sales reporting; create a separate payment-reconciliation monitor for the small set of material differences.

## 6. Limitations

- The dataset is an anonymised historical extract, not a live operational feed.
- The analysis identifies associations and patterns; it does not prove causal effects.
- Profit, discounts, marketing exposure, carrier identity, and inventory cost are not included, so profit and campaign ROI cannot be calculated.
- Product category names were retained as supplied in Portuguese; missing product categories were explicitly labelled `unknown`.

## 7. Reproducibility

The project notebooks document the complete sequence:

1. `01_data_ingestion_and_profiling.ipynb`
2. `02_cleaning_and_feature_engineering.ipynb`
3. `03_sales_and_operations_eda.ipynb`
4. `04_customer_rfm_segmentation.ipynb`

Outputs, including charts and tables used in the analysis, are saved under `outputs/`.
