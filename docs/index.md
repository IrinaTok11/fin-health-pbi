---
title: Financial Health — Power BI
---

<style>
  :root { --brand: #52837B; }

  .page-header .project-name,
  .page-header .project-tagline {
    color: #fff !important;
    text-shadow: none !important;
  }

  h1, h2, h3, h4, h5, h6 {
    color: var(--brand) !important;
    font-weight: 750 !important;    
    text-shadow: none !important;
  }
  h1 a, h2 a, h3 a, h4 a, h5 a, h6 a {
    color: var(--brand) !important;
    text-decoration: none;
  }

  .gallery{
    display:flex; gap:16px; justify-content:flex-start;
    align-items:flex-start; flex-wrap:wrap; margin:0; padding:0;
  }
  .gallery img{ width:48%; height:auto; margin:0; }
</style>

# Financial Health — Power BI

Portfolio preview of the interactive dashboard and KPI catalogue.

**Repository:** [github.com/IrinaTok11/fin-health-power-bi](https://github.com/IrinaTok11/fin-health-power-bi)  
**PBIX download:** [fin-health.pbix](https://github.com/IrinaTok11/fin-health-power-bi/raw/main/fin-health.pbix)

---

## Design variants (two pages)

| Variant | Intent | Where to use |
|---|---|---|
| **v1 — rounded cards** | Web/presentation look with soft background | On-screen portfolio |
| **v2 — flat, print-friendly** | Same numbers; flat skin for clean Word crops | Word **3.2 Analysis of liquidity ratios** |


Python portfolio:
**live page:** [irinatok11.github.io/fin-health-python](https://irinatok11.github.io/fin-health-python/)
**repository:** [github.com/IrinaTok11/fin-health-python](https://github.com/IrinaTok11/fin-health-python)


**Page 1 — rounded cards (v1)**
<p align="left">
  <img src="{{ 'cover.png' | relative_url }}" alt="Dashboard v1 — rounded cards" width="90%">
</p>

**Page 2 — flat cards (v2, print-friendly)**  
<p align="left">
  <img src="{{ 'cover2.png' | relative_url }}" alt="Dashboard v2 — flat cards for Word" width="90%">
</p>

---

## Highlights
- 12 KPIs across liquidity, stability, and profitability with norms and trends.
- Clean card layout with bands and trend arrows.
- Three-year comparison plus indexed micro-charts.
