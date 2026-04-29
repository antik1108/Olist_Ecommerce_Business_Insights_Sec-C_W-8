# NST DVA Capstone 2 - Project Repository

> **Newton School of Technology | Data Visualization & Analytics**
> A 2-week capstone focused on Python, Tableau, and GitHub-based business analytics for Brazilian e-commerce operations.

---

## Quick Start

If you are working locally:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

---

## Project Overview

| Field | Details |
|---|---|
| **Project Title** | Olist E-Commerce Business Insights |
| **Sector** | Retail / E-Commerce |
| **Team ID** | G-8 |
| **Section** | Section C |
| **Faculty Mentor** | Archit Raj |
| **Institute** | Newton School of Technology |
| **Submission Date** | April 2026 |

### Team Members

| Role | Name | Responsibility |
|---|---|---|
| Project Lead | Antik Mondal | GitHub coordination, repository structure, README documentation |
| Python Analysis Lead | Viraj Chafale | Statistical analysis, Python-based business analysis |
| Python ETL Lead | Anand Mishra | Data cleaning, transformation, ETL pipeline |
| Tableau Lead | Aadit Vachher | Tableau dashboard development and dashboard flow |
| Tableau Insights Lead | Sanchit Garg | EDA-driven dashboard insights and Tableau support |
| Strategy and Report Lead | Vridhi Chaudhary | Final report writing and documentation |
| PPT and Quality Lead | Viraj Chafale | Final presentation and delivery quality |

---

## Business Problem

Brazilian e-commerce marketplaces operate at scale, but customer experience depends heavily on reliable delivery, healthy seller operations, and consistent satisfaction outcomes. This project analyzes the Olist marketplace to understand how delivery performance, customer reviews, and customer value segments interact across orders, states, and product categories. The goal is to help business stakeholders identify where service quality is weakening and where operational improvements or retention efforts can create the highest impact.

**Core Business Question**

> How can Olist improve delivery reliability and customer satisfaction while prioritizing the customers, regions, and product categories that matter most to revenue?

**Decision Supported**

> This analysis supports decisions on logistics prioritization, category-level operational fixes, regional service improvement, and customer retention strategy using RFM segmentation.

---

## Dataset

| Attribute | Details |
|---|---|
| **Source Name** | Olist Brazilian E-Commerce Public Dataset |
| **Direct Access Link** | [Kaggle Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) |
| **Row Count** | 98,207 rows in the final master dataset |
| **Column Count** | 36 columns in `olist_master_dataset.csv` |
| **Time Period Covered** | September 2016 to September 2018 |
| **Format** | CSV |

**Raw Files Used**

- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_customers_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `product_category_name_translation.csv`

**Key Columns Used**

| Column Name | Description | Role in Analysis |
|---|---|---|
| `order_purchase_timestamp` | Timestamp when the order was placed | Time-series KPI tracking and trend analysis |
| `revenue` | Final order revenue | Revenue KPI, state/category contribution, Tableau cards |
| `review_score` | Customer review rating from 1 to 5 | Satisfaction analysis and delivery-impact testing |
| `delivery_time_days` | Total days taken to deliver the order | Delivery efficiency KPI |
| `delivery_delay_days` | Difference between actual and estimated delivery | Delay analysis and correlation testing |
| `is_late` | Boolean flag showing whether delivery was late | On-time delivery KPI and service-level analysis |
| `customer_state` | State of the customer in Brazil | Regional drill-down and operational comparison |
| `product_category_name_english` | Product category in English | Category-level insight generation |
| `customer_unique_id` | Unique customer identifier | RFM segmentation and repeat-customer analysis |

For full column definitions, see [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| KPI | Definition | Formula / Computation |
|---|---|---|
| On-Time Delivery Rate | Share of orders delivered on or before estimated date | `(1 - mean(is_late)) * 100` |
| Average Delivery Days | Average time between purchase and delivery | `mean(delivery_time_days)` |
| Average Review Score | Overall customer satisfaction level | `mean(review_score)` |
| Total Revenue | Total value generated from delivered orders | `sum(revenue)` |
| Average Order Value | Revenue earned per delivered order | `mean(revenue)` |
| RFM Segment Value | Customer quality based on recency, frequency, and spend | Derived in `data/processed/olist_rfm_segments.csv` |

**Current headline KPI values**

- On-time delivery rate: `93.35%`
- Average delivery time: `12.09 days`
- Average review score: `4.12`
- Total revenue analyzed: `13,494,400.74 BRL`
- Average order value: `137.42 BRL`
- Unique customers segmented: `94,990`

---

## Tableau Dashboard

| Item | Details |
|---|---|
| **Dashboard URL** | [Tableau Public](https://public.tableau.com/views/brazile-commerceanalysis/Overview?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link) |
| **Executive View** | The overview dashboard summarizes revenue, review score, delivery days, freight cost, order status, seller density, and review distribution in one high-level decision screen. |
| **Operational View** | The dashboard set supports deeper drill-down into order performance, seller geography, and customer-level or segment-level patterns for operational follow-up. |
| **Main Filters** | Review score bin, dashboard navigation between Overview, Orders, and Customers, plus interactive geographic/category exploration in Tableau. |

Supporting files:

- [`tableau/dashboard_links.md`](tableau/dashboard_links.md)
- [`tableau/screenshots/overview dashboard.png`](tableau/screenshots/overview%20dashboard.png)
- [`tableau/screenshots/orders dashboard.png`](tableau/screenshots/orders%20dashboard.png)
- [`tableau/screenshots/customer dashboard.png`](tableau/screenshots/customer%20dashboard.png)

---

## Key Insights

1. Olist maintains a strong overall on-time delivery rate of `93.35%`, but the remaining delayed orders create a disproportionate customer experience risk.
2. Late deliveries receive an average review score of only `2.27`, versus `4.25` for on-time orders, showing a major satisfaction penalty when logistics fail.
3. A Welch's t-test confirms this delivery-review gap is statistically significant, with `t = -98.38` and `p < 0.001`.
4. Delivery delay and customer review score have a meaningful negative relationship, with Pearson correlation `r = -0.2673`, indicating that larger delays usually reduce satisfaction.
5. Sao Paulo (`SP`) is the largest revenue-driving state by a wide margin, contributing `5.16M BRL`, making it a critical region for operational protection.
6. Rio de Janeiro (`RJ`) delivers high revenue (`1.81M BRL`) but has a weaker on-time rate (`88.23%`), which suggests strong commercial importance but operational inefficiency.
7. Maranhão (`MA`) has the weakest observed on-time rate among meaningful states at `83.02%`, indicating a clear regional delivery reliability problem.
8. `health_beauty`, `watches_gifts`, and `bed_bath_table` are among the highest-revenue categories, so improvements in these categories can move business outcomes faster than low-volume categories.
9. `office_furniture`, `baby`, and `electronics` show relatively weaker on-time performance among higher-volume categories, making them strong candidates for logistics intervention.
10. The marketplace is dominated by high-satisfaction reviews overall, but the review distribution is still highly sensitive to delivery execution.
11. RFM segmentation shows `Loyal Customers` as the largest segment (`29,607` customers), while `Champions` are fewer (`6,126`) but have the highest average monetary value at `248.6 BRL`.
12. The combined `At Risk`, `High Risk / Churn`, and `Lost` segments represent a large retention opportunity, showing that customer lifecycle management matters alongside operations.

---

## Recommendations

| # | Insight | Recommendation | Expected Impact |
|---|---|---|---|
| 1 | Late deliveries sharply reduce review scores | Prioritize SLA monitoring and carrier escalation for delayed orders before delivery promises are missed | Higher customer satisfaction and fewer negative reviews |
| 2 | Revenue-heavy states like `RJ` underperform on delivery reliability | Build region-specific logistics review for high-revenue but low-SLA states, starting with `RJ`, `BA`, and `MA` | Better retention in commercially important regions |
| 3 | A few high-volume categories drive both revenue and service risk | Create category-level logistics scorecards for `health_beauty`, `bed_bath_table`, `watches_gifts`, and `office_furniture` | Faster operational gains where scale is highest |
| 4 | Champions have the highest average spend | Launch VIP retention and repeat-purchase campaigns for `Champions` and `Loyal Customers` | Higher repeat revenue and stronger customer lifetime value |
| 5 | Large churn-risk segments remain in the base | Run win-back campaigns for `At Risk` and `High Risk / Churn` users with segment-specific offers and service recovery messaging | Improved reactivation and lower effective churn |

---

## Repository Structure

```text
Olist_Analysis/
|
|-- README.md
|
|-- data/
|   |-- raw/                         # Original Olist source files
|   `-- processed/                   # Cleaned exports for analysis and Tableau
|
|-- notebooks/
|   |-- 01_extraction.ipynb
|   |-- 02_cleaning.ipynb
|   |-- 03_eda.ipynb
|   |-- 04_statistical_analysis.ipynb
|   `-- 05_final_load_prep.ipynb
|
|-- scripts/
|   `-- etl_pipeline.py
|
|-- tableau/
|   |-- screenshots/
|   `-- dashboard_links.md
|
|-- reports/
|   |-- DVA_Project_Report.pdf
|   |-- project_report_template.md
|   `-- presentation_outline.md
|
|-- docs/
|   `-- data_dictionary.md
|
|-- insights/
|   `-- exported analysis visuals
|
|-- DVA-oriented-Resume/
`-- DVA-focused-Portfolio/
```

---

## Analytical Pipeline

The project follows a structured workflow:

1. **Extract** - Source Olist raw files and inspect their schema in [`notebooks/01_extraction.ipynb`](notebooks/01_extraction.ipynb).
2. **Clean and Transform** - Merge and clean the raw tables into analysis-ready outputs in [`notebooks/02_cleaning.ipynb`](notebooks/02_cleaning.ipynb).
3. **Explore** - Study delivery, revenue, and review behavior through exploratory analysis in [`notebooks/03_eda.ipynb`](notebooks/03_eda.ipynb).
4. **Analyze** - Run hypothesis testing, correlation analysis, and RFM segmentation in [`notebooks/04_statistical_analysis.ipynb`](notebooks/04_statistical_analysis.ipynb).
5. **Prepare for BI** - Validate exports for Tableau in [`notebooks/05_final_load_prep.ipynb`](notebooks/05_final_load_prep.ipynb).
6. **Visualize** - Publish the interactive Tableau dashboards for stakeholder consumption.
7. **Recommend** - Convert quantitative findings into business actions around logistics, customer experience, and retention.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Data cleaning, feature engineering, KPI calculation, and statistical analysis |
| Jupyter Notebooks | Stepwise analytical workflow and documentation |
| Pandas / NumPy | Data transformation and aggregation |
| SciPy | Statistical testing and correlation analysis |
| Matplotlib / Seaborn | Exploratory charts and supporting visuals |
| Tableau Public | Interactive dashboards and stakeholder presentation |
| GitHub | Version control, collaboration, and project documentation |

---

## Deliverables

- Final report: [`reports/DVA_Project_Report.pdf`](reports/DVA_Project_Report.pdf)
- Tableau dashboard links: [`tableau/dashboard_links.md`](tableau/dashboard_links.md)
- Data dictionary: [`docs/data_dictionary.md`](docs/data_dictionary.md)
- Processed customer segmentation outputs:
  - `data/processed/olist_rfm_segments.csv`
  - `data/processed/olist_rfm_summary.csv`

---

## Contribution Matrix

This table is aligned with available repository evidence (README role mapping, commit history, changed files, and deliverables under data/, notebooks/, scripts/, tableau/, and reports/).

| Team Member | Dataset and Sourcing | ETL and Cleaning | EDA and Analysis | Statistical Analysis | Tableau Dashboard | Report Writing | PPT and Viva |
|---|---|---|---|---|---|---|---|
| Antik Mondal | Owner | Support | Support | Support | Support | Support | Support |
| Anand Mishra | Support | Owner | Owner | Support | Support | Support | Support |
| Aadit Vachher | Support | Support | Support | Support | Owner | Support | Support |
| Viraj Chafale | Support | Support | Support | Owner | Support | Support | Owner |
| Vridhi Chaudhary | Support | Support | Support | Support | Support | Owner | Support |
| Sanchit Garg | Support | Support | Support | Support | Support | Support | Support |

_Declaration: We confirm that the above contribution details are accurate and verifiable through GitHub Insights, PR history, and submitted artifacts._

**Team Lead Name:** Antik Mondal

**Date:** 29 April 2026

---
## Summary

This project combines Python analytics, statistical testing, RFM segmentation, and Tableau storytelling to evaluate how delivery performance shapes customer satisfaction in the Olist marketplace. The final output is designed to help stakeholders improve logistics reliability, protect revenue-heavy regions and categories, and prioritize the most valuable customer segments.


