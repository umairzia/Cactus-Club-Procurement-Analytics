# Customer Analytics Dashboard

A full-stack data analytics project demonstrating ETL, data quality validation, and interactive visualization.

## What I Built

- **Data Pipeline** (Python/Pandas) — ingests transaction data, validates against data quality rules, generates compliance reports
- **Interactive Dashboard** (React/Recharts) — single-file, fully offline-capable visualization with multi-location drill-down
- **Methodology** — transaction-level analysis, aggregation, trend visualization

## Skills Demonstrated

- **Backend:** Python, Pandas, data wrangling, Excel file handling, data validation
- **Frontend:** React, Recharts (charting library), Tailwind CSS, responsive design
- **Full-stack:** End-to-end pipeline from raw data to production dashboard
- **Analysis:** Revenue trends, product mix analysis, seasonality detection, data quality scoring
- **Documentation:** Clear code comments, comprehensive README, reproducible pipeline

## How It Works

1. **Ingest** — reads raw transaction export with nested structure
2. **Validate** — applies business rules and completeness checks
3. **Aggregate** — computes monthly/weekly metrics and product rankings
4. **Visualize** — renders interactive dashboard with location filters, charts, and KPIs

## Running the Pipeline

```bash
pip install pandas openpyxl jupyter
jupyter notebook customer_data_pipeline.ipynb
```

The notebook outputs a data quality scorecard (Excel) and aggregated metrics used by the dashboard.

## Opening the Dashboard

`customer_dashboard.html` is a fully self-contained single file (684 KB). Just double-click to open in any browser. No server, no build step, no installation required.

## Tech Stack

- Python 3.13, Pandas, OpenPyXL
- React 18.3, Recharts 2.12, Tailwind CSS
- Jupyter Notebook

## What I Learned Building This

- Handling nested/hierarchical data from accounting systems
- Designing data validation rules for audit/compliance
- Building offline-capable web dashboards
- Balancing design aesthetics with analytical clarity
