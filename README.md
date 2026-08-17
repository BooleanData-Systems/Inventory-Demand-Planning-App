# Inventory & Demand Planning Accelerator

AI-powered inventory optimization and demand forecasting — all computed within
Snowflake from your existing order and inventory data, with zero data movement.

## How It Works

This app connects to tables you already maintain (orders, inventory levels, products)
and computes safety stock, reorder points, demand forecasts, stock status, and
supplier metrics internally. No pre-built forecast tables or analytics outputs required.

**You provide:**
- Your existing **orders/sales table** (order ID, product, date, quantity, price)
- Your existing **inventory levels** (product, warehouse, quantity on hand)
- Your existing **product master** (product ID, name, category, unit cost)
- Optionally: your **suppliers table** (supplier, lead time, country)

**The app computes:**
- Safety stock using service level z-score and demand variability
- Reorder points (ROP = daily demand x lead time + safety stock)
- Stock status classification (Healthy, Low Stock, Critical, Out of Stock, Overstocked)
- Demand forecasts via 3-month moving average with MAPE/bias metrics
- Inventory valuation at cost and price
- Date dimension derived from order history

## Consumer Setup

1. **Install the app** from the Marketplace.
2. **Bind table references** — grant SELECT on your orders, inventory, and products tables.
3. **Map your columns** — the setup wizard auto-detects common column names.
4. **Click "Build IDP Analytics"** — the pipeline computes all metrics internally.

No CREATE DATABASE or CREATE WAREHOUSE privileges are required.

## Required Data

| Table | Required? | Expected Columns |
|-------|-----------|-----------------|
| Orders | Yes | Order ID, product ID, order date, quantity, unit price |
| Inventory | Yes | Product ID, warehouse ID, quantity on hand |
| Products | Yes | Product ID, product name, category, unit cost |
| Suppliers | No | Supplier ID, name, lead time days |

Column names do not need to match exactly — the app provides an interactive mapping step
with auto-detection for common aliases.

## Computed Analytics

| Category | What's Computed |
|----------|----------------|
| Safety Stock | `z * std_demand * sqrt(lead_time)` at 95% service level |
| Reorder Point | `daily_demand * lead_time + safety_stock` |
| Stock Status | Derived from available qty vs safety stock and ROP |
| Demand Forecast | 3-month weighted moving average per product |
| Forecast Accuracy | MAPE and bias computed from forecast vs actual |
| Inventory Value | `quantity_on_hand * unit_cost` |

## Optional Columns

The pipeline handles missing optional data gracefully:
- No LINE_TOTAL → computed as quantity * unit_price
- No REGION → defaults to 'ALL'
- No GROSS_PROFIT → estimated at 30% of revenue
- No QUANTITY_AVAILABLE → uses quantity on hand
- No suppliers table → uses 14-day default lead time

## Support

For issues or questions, contact support@booleandata.io
