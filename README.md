# Nike Global Product Analysis

## 1. Project Title
Nike Global Product Dataset — Analysis & Dashboard

https://datastudio.google.com/reporting/c3e4949b-320c-49ae-bc8b-a93e3dc335be

## 2. Project Overview
This project analyzes a global Nike product feed (sample under 50MB) to explore pricing, availability, product mix, and market differences across countries. The workflow goes from raw CSV through cleaning and preparation to visualization or dashboarding (examples and dashboards may be stored under `DASHBOARD/`).

### Key Objectives
- Compare product prices and discounts across countries
- Analyze availability and stock signals by market and category
- Explore product mix (footwear, apparel, equipment) and sport tags
- Prepare cleaned data for visualization or Looker/Power BI dashboards

## 3. Project Structure
| Folder | File / Example | Description |
|---|---|---|
| Raw Dataset | `RAW DATASET/global_nike_under_50mb.csv` | Original CSV export (single snapshot). |
| Cleaned Dataset | `CLEANED DATASET/` | Place cleaned CSV / parquet / Excel outputs here. |
| Dashboard | `DASHBOARD/` | Dashboard assets, screenshots, and export files. |

## 4. Data Dictionary (selected fields)
| Column Name | Data Type | Description |
|---|---|---|
| `snapshot_date` | Date | Snapshot date for the record |
| `country_code` | Text | Two-letter country code (e.g. US, GB, JP) |
| `product_name` | Text | Product title |
| `model_number` | Text | Internal model identifier |
| `currency` | Text | Local currency code (USD, EUR, JPY, GBP) |
| `price_local` | Decimal | Local price value |
| `sale_price_local` | Decimal | Sale price if available |
| `discount_pct` | Decimal | Discount percentage (numeric) |
| `category` | Text | High-level category (FOOTWEAR / APPAREL / EQUIPMENT) |
| `subcategory` | Text | Category sub-type |
| `product_id` | Text | Product UUID |
| `sku` | Text | SKU identifier |
| `style_color` | Text | Style/color code |
| `brand_name` | Text | Brand (Nike / Jordan / etc.) |
| `available` | Boolean/Text | Availability flag (True/False) |
| `availability_level` | Text | HIGH / MEDIUM / LOW / OOS |
| `in_stock` | Boolean | Whether item is in stock in snapshot |
| `product_url` | URL | Product landing page |
| `image_url` | URL | Product image URL |
| `sport_tags` | Text | Sport categories (Running, Basketball, Soccer...) |
| `record_source` | Text | Data source / import method |

Full column list can be found in the CSV header.

## 5. Data Summary
- File: `RAW DATASET/global_nike_under_50mb.csv`
- Total records (rows): 83,492 (excluding header)
- Snapshot date example: 2026-03-19 (many records share this date)
- Countries observed: multiple markets (JP, GB, US, SI, IE, FI, etc.)
- Common categories: `FOOTWEAR`, `APPAREL`, `EQUIPMENT`

### Notable fields for analysis
- Price fields: `price_local`, `sale_price_local`, `discount_pct`
- Availability: `available`, `availability_level`, `in_stock`
- Identifiers for joins: `product_id`, `sku`, `gtin`, `catalog_sku_id`

## 6. Cleaning Notes
- Convert `price_local`, `sale_price_local`, and `discount_pct` to numeric (coerce errors).
- Normalize currencies if you want global price comparisons (requires exchange rates).
- Standardize `availability_level` and boolean fields (`available`, `in_stock`).
- Deduplicate using `product_id`/`sku` and resolve conflicting snapshots if multiple dates exist.
- Parse and normalize size fields (`nike_size`, `localized_size`, `size_conversion_id`) if doing size-level analysis.

## 7. Analytics / Dashboard View
Possible dashboards and views to build:
- Market overview: trip counts -> (here: product counts) and availability per country
- Price & discount analysis: average price, median price, discount rate per country and category
- Stock & availability: percent in-stock by SKU and country
- Product mix: top categories and sport tags by market
- Time-based analysis: if multiple snapshots exist, show availability changes over time

## 8. Tools Used
- pandas / Python for cleaning and EDA
- Jupyter Notebook for exploratory analysis
- Looker Studio / Power BI / Tableau for dashboards (CSV or cleaned Excel/parquet sources)

## 9. Quick Start (Python / pandas)
```python
import pandas as pd
df = pd.read_csv(r"RAW DATASET/global_nike_under_50mb.csv", encoding='utf-8')
# Basic clean
for c in ["price_local","sale_price_local","discount_pct"]:
    df[c] = pd.to_numeric(df[c], errors='coerce')
df['snapshot_date'] = pd.to_datetime(df['snapshot_date'], errors='coerce')
print(df.shape)
print(df[['country_code','category']].nunique())

# Example: average price by country and category
print(df.groupby(['country_code','category'])['price_local'].agg(['count','mean','median']).head())
```

## 10. Dashboard Assets / Screenshots
- Place dashboard screenshots or exported assets in `DASHBOARD/`.

## 11. Conclusion
This dataset provides a rich commerce feed suitable for price comparison, availability monitoring, category-level insights, and dashboarding. The identifier fields and multiple market coverage make it useful for cross-market analysis and inventory monitoring.

## 12. Future Enhancements
1. Add currency normalization using daily exchange-rate snapshots.
2. Produce cleaned outputs (CSV/parquet) under `CLEANED DATASET/` with typed columns.
3. Build a Looker/Power BI dashboard connected to the cleaned dataset.
4. Implement periodic snapshots and trend dashboards for availability changes.
5. Add geospatial analysis for regional assortment and demand.

---

If you'd like, I can also create a Jupyter notebook with EDA and a cleaned CSV saved to `CLEANED DATASET/`. Which would you like me to do next?
