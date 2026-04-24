# Inventory & Demand Planning Accelerator

AI-powered inventory optimization and demand forecasting platform built as a Snowflake Native App. Connect your supply chain data for real-time insights across five intelligence modules.

## Features

### Inventory Overview
- Real-time KPIs: inventory rate, stockout rate, turnover, service level, forecast accuracy, working capital %
- Monthly demand trends, revenue trends, and stock status distribution
- Revenue and profit breakdowns by product

### Inventory Deep Dive
- Per-product inventory status with stock, safety stock, reorder point, and risk levels
- Units sold and revenue analysis with filters by category, subcategory, product, region, year, month
- Best and worst performers by profit with margin analysis
- Product intelligence with ABC-XYZ classification and strategic recommendations
- Category monthly breakdowns with best/worst product identification

### Demand Intelligence
- Seasonally-adjusted demand forecasting with configurable horizon (monthly/yearly)
- Forecast vs actual backtesting with accuracy metrics (MAPE, bias)
- Profit forecasting: expected revenue, cost, and profit per product
- Seasonal demand pattern analysis with peak/trough identification
- Cortex AI-powered demand narratives

### Action Center — PO Scheduler
- Smart purchase order engine using ROP and EOQ calculations
- Orders categorized by urgency: Critical/Today, This Week, This Month, In Stock
- Per-product PO suggestions with quantities, dates, values, and profit/loss projections
- AI-generated purchase order recommendations via Cortex

### IDP Assistant
- Executive brief generation powered by Snowflake Cortex AI
- Free-form Q&A about your inventory and demand data
- Preset quick questions for common scenarios

## Required Data Tables

After installing, bind these 7 table references to your data:

| Reference | Key Columns |
|-----------|-------------|
| Fact Inventory | PRODUCT_ID, WAREHOUSE_ID, QUANTITY_ON_HAND, QUANTITY_AVAILABLE, REORDER_POINT, SAFETY_STOCK, STOCK_STATUS, INVENTORY_VALUE_AT_COST, INVENTORY_VALUE_AT_PRICE |
| Fact Demand | ORDER_ID, PRODUCT_ID, ORDER_DATE, QUANTITY, UNIT_PRICE, LINE_TOTAL, ORDER_STATUS, REGION, IS_ON_TIME, GROSS_PROFIT |
| Fact Forecast | PRODUCT_ID, FORECAST_DATE, FORECAST_QTY, ACTUAL_QTY, MAPE_PCT, BIAS_PCT, CONFIDENCE_LEVEL |
| Dim Product | PRODUCT_ID, PRODUCT_NAME, CATEGORY, SUBCATEGORY, UNIT_COST, SUPPLIER_ID |
| Dim Warehouse | WAREHOUSE_ID |
| Dim Supplier | SUPPLIER_ID, SUPPLIER_NAME, COUNTRY, LEAD_TIME_DAYS, RELIABILITY_SCORE, SUPPLIER_TIER, IS_ACTIVE |
| Dim Date | DATE_KEY, YEAR_MONTH, MONTH_NAME, YEAR, MONTH |

## Permissions

The app requests SELECT access on bound tables. All analytics run in-place on your Snowflake warehouse. Cortex AI functions (optional) require access to `SNOWFLAKE.CORTEX.TRY_COMPLETE`.

## Version History

| Version | Date | Notes |
|---------|------|-------|
| 1.0.0 | 2026-04-24 | Initial marketplace release |
