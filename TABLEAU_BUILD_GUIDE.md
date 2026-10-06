Tableau Public Dashboard: Build Guide (Beginner Version)

This walks through every click. No prior Tableau memory needed.

A quick note before you start: I cannot see or control your Tableau
window myself, so there are no real screenshots here, just exact button
and panel names, matching what you already see on your own screen.

## 0. Five words you need to know first

- Data Source: one table of data (one CSV, in our case). Tableau needs
  to know which data source a sheet is "looking at" before any field
  will show up.
- Sheet: one single chart. You will make 9 sheets total (5 charts + 4
  KPI number tiles).
- Dimension: a text/category field (example: category, seller_id).
  Shown in blue.
- Measure: a number field you can sum/average (example: total_revenue).
  Shown in green.
- Dashboard: the final single page that combines several Sheets
  together. You make this last.

## 1. Fix: why Sheet 1 only shows gold_category_sell_through fields

This is the exact problem in your screenshots. Here is why it happens
and the guaranteed fix.

Tableau only shows a Sheet the fields from whichever ONE data source is
currently "active" for that sheet. Right now all 5 CSVs got loaded into
one combined data source, but only gold_category_sell_through.csv was
actually placed on the canvas (that grey box in your Data Source tab
screenshot), so it is the only one "active."

Fix, once, right now:

1. Click the Data Source tab at the very bottom-left of the window
   (you can see it in your first screenshot, next to "Sheet 1").
2. In the left sidebar, under Connections, click
   gold_delivery_time_by_seller — this selects that connection.
3. You will now see it as a small grey box appear in the empty canvas
   area at the top. Do not drag it onto the other box. Leave it sitting
   on its own. Leaving tables unconnected to each other is correct
   here — these 5 tables have nothing in common to join on.
4. Repeat step 2 and 3 for the other 3 remaining CSVs:
   gold_discount_depth_vs_volume, gold_revenue_by_category,
   gold_seller_performance (gold_category_sell_through is already
   there).
5. You should now see 5 separate small grey boxes sitting in the
   canvas, not touching each other.

That's it. This one-time setup makes every table's fields available.
Now, for each new Sheet you make, you just tell Tableau which of the 5
boxes to use (step-by-step below).

## 2. How to pick which table a Sheet uses

Every time you make a new sheet:

1. Right-click the Sheet 1 tab (bottom of window) and choose
   Rename — give it a name like "Category Revenue" so you don't lose
   track.
2. Look at the Data pane, top-left. Above the Dimensions/Measures list
   there is a small database-cylinder icon and a data source name —
   this is the active table. If it is showing the wrong table, click
   directly on that name and a dropdown/list of all 5 tables appears
   (or the tables are listed as separate collapsible headers in that
   same panel — click the one you want).
3. Once the right table's name is showing there, Dimensions and
   Measures below it update to match that table.

You will repeat this "pick the right table" step for every single sheet
below.

## 3. Build the 5 chart sheets

For each one: make a new sheet (the small "+" icon next to the sheet
tabs at the very bottom, right next to "Sheet 1"), rename it, pick the
right table (step 2 above), then drag the fields exactly as listed.

Dragging fields: click and hold a field name in the Dimensions or
Measures list on the left, drag it onto the Columns shelf or Rows
shelf (the two horizontal bars at the top of the empty chart area,
labeled "Columns" and "Rows"), or directly onto the little squares
in the Marks card (Color / Size / Text / Detail / Tooltip) just left
of the chart area.

### Sheet: "Category Revenue" (table: gold_category_sell_through)

1. Drag category to the Rows shelf.
2. Drag total_revenue to the Columns shelf.
3. Top-right panel "Show Me": click the horizontal-bars icon (looks
   like a bar chart lying on its side) to make it a horizontal bar
   chart, sorted longest to shortest.
4. To sort: click the little sort icon that appears when you hover
   over the total_revenue axis at the top of the chart (a small
   ascending-bars icon), click it once or twice until it's sorted
   biggest to smallest.

### Sheet: "Avg Price by Category" (same table: gold_category_sell_through)

1. New sheet, rename, pick gold_category_sell_through again.
2. Drag category to Rows.
3. Drag avg_price to Columns.
4. Pick the horizontal bar chart from Show Me, same as above.

### Sheet: "Partner Performance" (table: gold_seller_performance)

1. New sheet, rename "Partner Performance", pick
   gold_seller_performance as the active table.
2. Drag total_revenue to Columns.
3. Drag on_time_rate to Rows.
4. Drag total_orders onto the Size box in the Marks card (bubble size).
5. Drag avg_delivery_days onto the Color box in the Marks card.
6. In Show Me, pick the scatter plot (looks like scattered dots).
   This is your "who are our best partners" view — best sellers land
   top-right: high revenue, high on-time rate.

### Sheet: "Pricing Dynamics" (table: gold_discount_depth_vs_volume)

1. New sheet, rename "Pricing Dynamics", pick
   gold_discount_depth_vs_volume as the active table.
2. Drag avg_discount_pct to Columns.
3. Drag units_sold to Rows.
4. Drag category onto the Color box in the Marks card.
5. Pick the scatter plot from Show Me.
   Caption to remember for later: Olist has no list-price field, so
   avg_discount_pct is each product's price compared to its own
   average price, not a real store discount. Worth saying out loud if
   anyone asks about this chart.

### Sheet: "Delivery Time by Seller" (table: gold_delivery_time_by_seller)

1. New sheet, rename "Delivery Time", pick
   gold_delivery_time_by_seller as the active table.
2. Drag seller_id to Rows.
3. Drag avg_delivery_days to Columns.
4. Pick the horizontal bar chart from Show Me, sort ascending (fastest
   first).
5. This table has ~1,766 sellers, so also: right-click the seller_id
   pill on the Rows shelf, no direct "top N" there — instead, drag
   avg_delivery_days onto the Filters box (top-left panel, "Filters"),
   choose "At Least"/"At Most" or use the "Top" tab in the filter
   dialog to keep just the top 15 and bottom 15 by avg_delivery_days,
   so the chart is readable instead of 1,766 bars.

## 4. Build the 4 KPI number tiles

Tableau Public does not have a dedicated "KPI card" object, so the
standard trick is: one sheet, one giant number, no chart lines around
it.

For each of the 4 below: new sheet, rename it, pick the table noted,
drag only that one field onto the Text box in the Marks card (not
Columns or Rows — leave those empty).

1. "KPI Total Revenue" — table gold_revenue_by_category, field
   total_revenue (drag to Text). Right-click the pill that appears in
   Marks > Text, choose Measure > Sum if it is not summed already.
2. "KPI Sellers Tracked" — table gold_seller_performance, field
   seller_id (drag to Text), then right-click that pill and change
   its aggregation to Count (Distinct) so it counts unique sellers.
3. "KPI On-Time %" — table gold_delivery_time_by_seller, field
   on_time_rate (drag to Text), right-click and set aggregation to
   Average.
4. "KPI Avg Delivery Days" — table gold_delivery_time_by_seller,
   field avg_delivery_days (drag to Text), aggregation Average.

To make the number big: with Text selected in the Marks card, click
the "T" Text button that appears (or right-click in the blank chart
area and choose Format), and bump the font size up to 24-36pt.

## 5. Assemble the dashboard

1. Click the "New Dashboard" icon — it's the small icon right next to
   the sheet-tab "+" button at the bottom (looks like 4 small
   rectangles), or Dashboard menu (top) > New Dashboard.
2. On the left, under "Sheets," you'll see all 9 sheets you made
   listed. Drag them one at a time onto the blank canvas on the right.
3. Suggested layout: the 4 KPI sheets in a row across the top, then
   "Partner Performance" and "Pricing Dynamics" side by side below
   that, then "Delivery Time" and one of the category sheets side by
   side below that.
4. To add a title and the captions from the earlier build guide: drag
   a "Text" object (left sidebar, under "Objects") onto the canvas
   above or below each chart, click into it, and type the caption.
5. Dashboard title (top of the page): double-click where it says
   "Dashboard 1" at the top and rename it to something like
   "E-Commerce Supply, Partner and Pricing Analytics."

## 6. Publish

1. File menu (top-left) > Save to Tableau Public As...
2. Sign in with the account you created.
3. Give it a name and click Save/Publish.
4. Tableau opens your browser to the published page — copy that URL,
   that's your dashboard link to send back.
