Tableau Public Dashboard: Build Guide

Once the Databricks notebook has run and you have downloaded the 5 gold
CSVs into gold_data/, build the dashboard in Tableau Public Desktop.

## 1. Connect

Open Tableau Public Desktop, Connect, Text File, select all 5 CSVs
from gold_data/:
- gold_seller_performance.csv
- gold_category_sell_through.csv
- gold_discount_depth_vs_volume.csv
- gold_delivery_time_by_seller.csv
- gold_revenue_by_category.csv

They are independent (no relationships needed) since each gold table
already answers one question on its own, so build one sheet per table
rather than a single blended model.

## 2. KPI header (top of dashboard)

Four single-value text tiles, one calculated field each pulling from
the relevant gold table:
- Total Revenue: SUM(total_revenue) from gold_revenue_by_category
- Sellers Tracked: COUNTD(seller_id) from gold_seller_performance
- On-Time Delivery %: AVG(on_time_rate) from gold_delivery_time_by_seller
- Avg Delivery Days: AVG(avg_delivery_days) from gold_delivery_time_by_seller

## 3. View 1: Partner (Seller) Performance

Sheet from gold_seller_performance:
- Scatter plot: total_revenue (x) vs on_time_rate (y), size =
  total_orders, color = avg_delivery_days. This is the "who are our
  best partners" view: the top-right quadrant is the high-revenue,
  reliable-delivery sellers.
- Caption: "Seller-level revenue plotted against on-time delivery rate.
  Bubble size is order volume; darker bubbles deliver slower."

## 4. View 2: Pricing Dynamics (Discount Depth vs Volume)

Sheet from gold_discount_depth_vs_volume:
- Scatter plot: avg_discount_pct (x) vs units_sold (y), color =
  category
- Caption: "Products priced below their own average (a proxy for
  discounting, since Olist has no list-price field) plotted against
  units sold, testing whether deeper effective discounts actually move
  volume in this catalog."

## 5. View 3: Category Trends

Combine gold_category_sell_through and gold_revenue_by_category (same
grain, category) via a blend, or just build two sheets:
- Bar chart: category (rows, sorted by revenue) vs total_revenue
- Bar chart: category vs avg_price, showing which categories are
  high-volume/low-price vs low-volume/high-price
- Caption: "Revenue concentration by category, with average price per
  category to separate high-ticket from high-frequency categories."

## 6. View 4: Delivery Time by Seller

Sheet from gold_delivery_time_by_seller:
- Bar chart: top and bottom 10 sellers by avg_delivery_days
- Caption: "Slowest and fastest delivering partners by average delivery
  days, filtered to sellers with 5+ orders to avoid noise from
  one-off sellers."

## 7. Assemble the dashboard

New Dashboard, drag all 4 sheets onto one canvas, KPI header across the
top, a 2x2 grid of views below. Add a title: "E-Commerce Supply,
Partner and Pricing Analytics, Olist Dataset".

## 8. Publish

File, Save to Tableau Public As..., sign in, publish. Copy the
resulting public URL into README.md.
