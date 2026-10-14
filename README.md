# DCFs

Discounted cash flow (DCF) valuation models in Excel.

Part of **Independent Financial Modeling Projects** (May 2024 – Present):

- Built 5-year DCF models for multiple tech companies, comparing implied to market price to form buy/hold/sell views
- Ran WACC and terminal growth sensitivity tables in Excel to define a defensible per-share implied value range

**Where to find it:** the 5-year tech-company DCFs are the MU and GOOGL models (implied value vs. market price); WACC and terminal growth sensitivity tables are in GOOGL (WACC vs. g) and the NBA Happy Hour Co models (WACC vs. perpetuity growth). The NBA models and the tutorial workbook are practice / case-study material.

## Index

| Model | Company | Method | Headline result |
|---|---|---|---|
| [MU DCF.xlsx](MU%20DCF.xlsx) | Micron Technology (MU) | 5-year unlevered FCF, 11.49% WACC | $390.14/share, ~32% upside vs. ~$294 |
| [GOOGL DCF.xlsx](GOOGL%20DCF.xlsx) | Alphabet (GOOGL) | FY2026E–FY2030E unlevered FCF, perpetuity growth, mid-year discounting | $118.21/share base case vs. $353.78 (11.7% WACC, 2.5% terminal growth) |
| [NBA BASIC - Happy Hour Co - DCF model v2.xlsx](NBA%20BASIC%20-%20Happy%20Hour%20Co%20-%20DCF%20model%20v2.xlsx) | Happy Hour Co | Perpetuity growth DCF, 8.5% WACC, 0.5% TGR | ~358.8c/share (+117.5% vs. 165c) |
| [NBA ADVANCED - Happy Hour Co - DCF model v2.xlsx](NBA%20ADVANCED%20-%20Happy%20Hour%20Co%20-%20DCF%20model%20v2.xlsx) | Happy Hour Co | Perpetuity growth and exit EBITDA multiple (8.5x) | ~297c (perpetuity) / ~390c (exit multiple) |
| [NBA Happy Hour Co - DCF model - Task 4 - Revised Template.xlsx](NBA%20Happy%20Hour%20Co%20-%20DCF%20model%20-%20Task%204%20-%20Revised%20Template.xlsx) | Happy Hour Co | Same DCF with a revised Year 1 revenue case (1,100) | ~328.6c/share (+99.1% vs. 165c) |
| [2024.08.-DCF-Tutorial-Part-1.xlsx](2024.08.-DCF-Tutorial-Part-1.xlsx) | Reference tutorial | DCF, WACC, shares, segments, IS, CFS, CapEx | Reference workbook |

## Model notes

- **MU** – Thesis: HBM-driven AI memory demand and operating leverage. Sheets: Executive Summary, DCF, WACC, Income Statement, Cash Flow Statement.
- **GOOGL** – Bear / base / bull case selector, WACC build-up (CAPM), and sensitivity tables for WACC vs. terminal growth, growth vs. margin, and beta vs. risk-free rate. Historicals from the Annual Financial sheet.
- **NBA models** – Three-statement forecast feeding a DCF with a WACC / terminal growth sensitivity grid and implied offer price.
