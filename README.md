# DAX vs. MDAX — German Equity Market Analysis (H1 2026)

*[Deutsche Version](README.de.md)*

A data analytics portfolio project comparing the performance, risk, and market breadth of Germany's two main equity indices — the **DAX** (40 large-cap constituents) and the **MDAX** (50 mid-cap constituents) — over the first half of 2026 (2025-12-30 to 2026-06-30).

The project has two parts:
1. A **Python/Jupyter notebook** ([`dax_mdax_analysis.ipynb`](dax_mdax_analysis.ipynb)) that pulls, cleans, and analyzes daily price data for both indices and their constituents.
2. A **Power BI dashboard** built on top of the notebook's output, with 5 pages for interactive exploration.

## Key Findings

- **Return:** MDAX outperformed DAX in H1 2026 (**+2.83%** vs. **+0.56%**, a difference of **-2.27 pp**).
- **Risk:** MDAX carried higher risk — annualized volatility of **22.1%** vs. **18.7%** for DAX. Maximum drawdown can be read two ways: at the **index level** (the index's own price series), it was **-14.4%** (MDAX) vs. **-12.3%** (DAX); at the **constituent level** (the single worst-performing company within each index), it was **-52.25%** (MDAX) vs. **-50.21%** (DAX). The Power BI dashboard's "Max Drawdown" cards show the constituent-level figures.
- **Breadth:** Gains were broad-based, not concentrated in a few names — **55–56%** of companies in both indices posted a positive H1 return.
- **Extremes:** Strongest performers were Aixtron (**+201.0%**, MDAX) and Infineon Technologies (**+108.96%**, DAX). Weakest were KION Group (**-43.8%**, MDAX) and Rheinmetall (**-37.2%**, DAX).
- **Index composition note:** Hochtief joined the DAX on 2026-06-22, replacing Porsche SE, which moved to the MDAX. Both indices are modeled with their post-swap composition (DAX: 40 / MDAX: 50).

No market-cap weighting was computed in this project, so no claims are made about which specific companies drove index-level performance — the findings above describe the constituent-level data only.

## Data & Methodology

- **Source data:** daily OHLC price data for the DAX index, the MDAX index, and all individual constituents of both, covering 2025-12-30 through 2026-06-30.
- **Processing:** cleaned and forward-filled in Python (pandas), with derived metrics computed per company: total return, annualized volatility, maximum drawdown, and rank within index.
- **Exports:** four CSVs feed the Power BI model —
  - `daily_market_data.csv` — daily prices and returns, indices and constituents
  - `company_metadata.csv` — company name, sector, index membership, ticker
  - `company_summary.csv` — H1 summary stats per company (return, volatility, drawdown, rank)
  - `monthly_summary.csv` — monthly returns per index

## Power BI Dashboard

The dashboard uses a star schema (`Dim_Company`, `Dim_Date`, `Fact_DailyMarketData`, `Fact_CompanySummary`, `Fact_MonthlySummary`) and is built across 5 pages:

| Page | What it shows |
|---|---|
| **1. Market Overview** | Indexed performance (base = 100), H1 return KPIs, monthly returns by index |
| **2. Risk and Performance** | Best/worst trading days per index, maximum drawdown, return vs. volatility by company |
| **3. Market Breadth** | Share of positive companies, index vs. median return, distribution of company returns |
| **4. Sector Explorer** | Sector-level return and market share, split by DAX/MDAX, top/bottom 5 sectors |
| **5. Company Explorer** | Full company-level table with slicers (index, sector, company), top/bottom 5 performers |

### Screenshots

#### 1. Market Overview
Indexed performance (base = 100) for DAX vs. MDAX across H1 2026, headline return KPIs, and monthly returns by index.

![Market Overview](images/01-market-overview.png)

#### 2. Risk and Performance
Best/worst single trading day per index, maximum drawdown cards, and a scatter chart plotting return against volatility for every company.

![Risk and Performance](images/02-risk-performance.png)

#### 3. Market Breadth
Share of companies with a positive H1 return, index return vs. median company return, and a histogram of how company returns are distributed.

![Market Breadth](images/03-market-breadth.png)

#### 4. Sector Explorer (DAX)
Top 5 / bottom 5 sectors by return for the selected index, plus a matrix comparing return and market share by sector across DAX and MDAX side by side. Index slicer set to DAX.

![Sector Explorer](images/04-sector-explorer.png)

#### 5. Sector Explorer (MDAX)
Same page as above, with the index slicer switched to MDAX — shows MDAX's own top/bottom performing sectors while the matrix at the bottom keeps both indices visible.

![Sector Explorer detail](images/05-sector-explorer-detail.png)

#### 6. Company Explorer
Full company-level table filterable by index, sector, and company, plus top 5 / bottom 5 performer charts.

![Company Explorer](images/06-company-explorer.png)

#### 7. Data Model (Star Schema)
The Power BI data model: `Dim_Company`, `Dim_Date`, `Fact_DailyMarketData`, `Fact_CompanySummary`, `Fact_MonthlySummary`, and the relationships between them.

![Star schema](images/07-star-schema.png)

## Tools

- Python (pandas, Jupyter)
- Power BI (DAX, Power Query, data modeling)
- Claude (Anthropic) — used as an AI assistant during development (debugging, documentation)

## Author

Amir ([@Amirhouschang](https://github.com/Amirhouschang))
