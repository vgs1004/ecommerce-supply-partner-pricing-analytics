E-Commerce Supply, Partner and Pricing Analytics

A Databricks SQL pipeline (raw, cleaned, gold layers) feeding a Tableau
Public dashboard on partner performance and pricing dynamics, built on
the Brazilian E-Commerce Public Dataset by Olist (Kaggle).

## What it is

- Public dataset: Olist Brazilian E-Commerce
  (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), around
  100k orders, 2016 to 2018. No proprietary or employer data.
- A three-layer SQL pipeline in Databricks: raw tables loaded from the
  source CSVs, a cleaned joined view, and five gold aggregate tables.
- A Tableau Public dashboard built from the gold layer.

## Tools used

- Databricks Community Edition (Spark SQL, Delta tables)
- SQL (joins, window functions, aggregation) for all three layers
- Tableau Public (calculated fields, scatter plots, dashboard design)

## What it shows

Raw layer: the 7 source CSVs loaded as-is into Delta tables under the
olist_raw schema.

Cleaned layer: one joined view (cleaned_order_items) combining order
items, orders, sellers, and products with English category names and
computed delivery timing (delivery_days, is_on_time).

Gold layer, five tables:
- gold_seller_performance: revenue, order count, delivery speed, and
  on-time rate per seller
- gold_category_sell_through: units sold, revenue, and average price
  per category
- gold_discount_depth_vs_volume: how far each product's price sits
  below its own average selling price, against units sold (a
  documented proxy for discounting, since Olist has no list-price
  field to measure a true discount against)
- gold_delivery_time_by_seller: average delivery days and on-time rate
  per seller
- gold_revenue_by_category: total revenue and share of revenue per
  category

Dashboard: a KPI header (total revenue, sellers tracked, on-time
delivery %, average delivery days) plus four views covering partner
performance, pricing dynamics, category trends, and delivery time by
seller.

## Files

| File | Purpose |
|---|---|
| notebook/olist_supply_partner_pricing_analytics.sql | The full Databricks notebook (raw, cleaned, gold layers), importable directly into Databricks |
| gold_data/ | The five gold CSVs exported from Databricks, used as the Tableau data source |
| TABLEAU_BUILD_GUIDE.md | Exact sheets, fields, and captions used to build the dashboard |
| screenshots/ | Dashboard views |

## Links

- Tableau Public dashboard: (added once published)
- GitHub repo: (added once pushed)

Note: the raw Olist CSVs are not included in this repo (available free
from the Kaggle dataset page linked above); run the notebook's raw-layer
cell after uploading them to Databricks to reproduce the pipeline.
