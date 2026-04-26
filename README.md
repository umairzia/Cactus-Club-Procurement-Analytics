# Cactus Club Procurement Analytics

A data pipeline and interactive dashboard for analyzing procurement patterns across Cactus Club Cafe's three Toronto locations (Sherway Gardens, First Canadian Place, Yonge St).

## Overview

This project processes transaction data from a multi-location customer, performs data quality validation, and generates an interactive dashboard to surface revenue trends, product popularity, and order cadence by location. The intent is to support account management, pricing strategy, and cross-sell opportunities.

**Data coverage:** 12-month period  
**Scope:** Multiple transactions and SKU purchases across multiple locations

## Key Capabilities

This analysis uncovers:
- Revenue concentration and location-level performance variance
- Top and bottom performers in the product mix
- Ordering frequency patterns and seasonality
- Data quality issues at the transaction and line-item level
- Cross-location comparison for account strategy optimization

## What's in This Repo

```
├── customer_data_pipeline.ipynb            # Data ingestion & quality validation pipeline
├── customer_dashboard.html                 # Standalone interactive dashboard (fully offline)
├── customer_dashboard.jsx                  # React dashboard source (for development)
├── raw_data.xlsx                           # Raw transaction data (input — not included for security)
├── dq_scorecard.xlsx                       # Data quality scorecard output (not included)
├── profiling_summary.xlsx                  # Profiling summary output (not included)
└── README.md                               # This file
```

**Note:** Raw data and generated outputs are excluded from version control for security. Only the pipeline code and dashboard source are tracked.

## The Dashboard

**`cactus_dashboard.html`** is a self-contained, single-file interactive dashboard. No installation, login, or internet required after first load.

### Features
- **Tab navigation** — switch between all-customer roll-up and individual location views
- **Revenue trend** — time-period revenue chart (multi-faceted visualization when viewing aggregate)
- **Order cadence** — periodic order count visualization with average line
- **Product mix** — top and bottom SKUs by volume and revenue contribution
- **KPIs** — total revenue, order count, average order value, order frequency metrics per location
- **Comparison view** — all-locations display shows side-by-side cards with revenue share and performance metrics

### How to Use
1. **Download** `cactus_dashboard.html`
2. **Open** in any modern browser (Chrome, Safari, Firefox, Edge) — just double-click
3. **Interact** — click tabs to filter by location, hover charts to inspect values, click location cards to drill down

**Note:** The dashboard fetches web fonts on first load. After that, it's fully cached and works offline. System fonts render as fallback if remote fonts are blocked by your network.

## The Pipeline

**`Cactus_KT_Data.ipynb`** (Jupyter Notebook, Python 3.13) processes raw transaction data and generates data quality reports.

### What It Does
1. **Ingestion** — reads raw `Cactus_2025.xlsx`, promotes first row to header, flattens nested transaction/line-item structure
2. **Validation** — applies data quality rules (gross ≈ net reconciliation, completeness checks on stock codes and net amounts)
3. **Aggregation** — generates monthly scorecard with:
   - Transaction count
   - Line item count
   - Gross sales
   - Field completeness %
   - Rule-pass rate (data integrity)
4. **Output** — writes `Cactus_2025_DQ_scorecard.xlsx` for audit/compliance

### How to Run
```bash
# Install dependencies
pip install pandas openpyxl

# Run the notebook
jupyter notebook Cactus_KT_Data.ipynb
```

Or with conda:
```bash
conda env create -f environment.yml
conda activate cactus
jupyter notebook Cactus_KT_Data.ipynb
```

### Input Requirements
- **Raw transaction export** — structured export from accounting system, with first row as headers
  - Nested columns expected: transaction-level fields and nested line-item detail
  - Required fields: transaction ID, gross amount, date, location, type, description, quantity, stock code

### Outputs Generated
- **Data quality scorecard** — period-by-period data quality metrics (completeness, validation rule pass rates)
- **Dashboard data artifacts** — aggregated revenue, product rankings, and frequency analysis (used by the dashboard)

## Tech Stack

- **Data pipeline:** Python 3.13+, Pandas, OpenPyXL
- **Dashboard frontend:** React 18.3+, Recharts 2.12+, Tailwind CSS
- **Design system:** Serif display, sans-serif body, monospace data font

## Updating with New Data

When you receive new transaction data:

1. **Replace source file** with the new data export
2. **Run the notebook** to generate a fresh data quality scorecard:
   ```bash
   jupyter notebook customer_data_pipeline.ipynb
   ```
3. **Recompute dashboard data** — regenerate the aggregated metrics
4. **Rebuild the HTML dashboard** with updated data points

*(The HTML file contains all computed data as embedded JavaScript constants.)*

## Known Limitations

- **Data quality artifacts** — some line items are placeholder/in-transit rows that should be filtered at source
- **Partial period coverage** — final period in the dataset is incomplete, so metrics for that period are not representative of a full cycle
- **DQ scorecard accounting** — the gross sales field in the data quality scorecard may differ from actual revenue depending on deduplication methodology; ensure you understand which measure is used for reporting
- **Raw product nomenclature** — SKU descriptions from the source system are verbose and contain formatting artifacts; a cleaner product master would improve readability

## Future Enhancements

- Add day-of-week analysis to spot intra-week ordering patterns
- Build cost-of-goods analysis to show margin by product and location
- Implement price variance checks (same SKU should have consistent unit pricing)
- Create automated email alerts for anomalies (e.g., orders below/above historical average)
- Connect to a real database (PostgreSQL, Snowflake) instead of static files for real-time reporting
- Add customer behavior cohorts (e.g., fast-movers vs. slow-movers, seasonal vs. steady)

## Questions?

For issues with the pipeline, DQ rules, or dashboard functionality, feel free to open an issue or reach out directly.

---

**Version:** 1.0  
**Dashboard:** Production-ready, fully offline capable
