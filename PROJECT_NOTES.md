# Project Notes

Internal notes for maintaining **Integra LLC — Financial Health Dashboard (Power BI)**.

---

## Quick links
- Live page: https://IrinaTok11.github.io/fin-health-power-bi/
- Repository: https://github.com/IrinaTok11/fin-health-power-bi
- PBIX: [/fin-health.pbix](/fin-health.pbix) · [direct download](/fin-health.pbix?raw=1)
- Docs: [/docs/index.md](/docs/index.md) · [/docs/methodology.md](/docs/methodology.md)
- DAX: [/dax/](/dax/) · Deneb specs: [/deneb/](/deneb/)
- Screenshots: [/assets/dashboard_cover.png](/assets/dashboard_cover.png) · [/assets/dashboard_cover2.png](/assets/dashboard_cover2.png)

---

## What’s shipped
- Two report pages: **v1 (rounded/web)** and **v2 (flat/print)** using the **same model and measures**.
- Sample/anonymized Excel in `/data/`. DAX measures in `/dax/`. Deneb JSON specs in `/deneb/`.

---

## Maintenance checklist (before a release)
- [ ] PBIX opens and **Refresh** completes without errors.
- [ ] Data source path points to `data/integra_financial_analysis.xlsx` (repo-relative).
- [ ] Pages are clearly named: `Dashboard v1 (Rounded)` and `Dashboard v2 (Flat/Print)`.
- [ ] README renders both screenshots and links resolve.
- [ ] `docs/methodology.md` includes the v1/v2 table and matches current styling.
- [ ] Deneb specs present and valid:  
      `kpi_bars_numeric.vl.json`, `kpi_bars_percent.vl.json`,  
      `legend_status.vl.json`, `row_labels.vl.json`,  
      `trend_indexed.vl.json`, `trend_pnl.vl.json`.
- [ ] DAX style: comma-separated arguments; naming pattern `grp__KPI__SubKPI__MeasureName`.
- [ ] `/assets` contains only images that are actually used (`dashboard_cover*.png`).
- [ ] LICENSE and contact info in README are up to date.

---

## Change log
- **v1.1 — 2025-08-24**: Added **Page 2 (flat/print)**; cleaned screenshots; updated README and docs/methodology.
- **v1.0 — 2025-08-22**: Initial public release (dashboard v1, DAX + Deneb, sample data).

---

## Backlog (next)
- Sector benchmarks (peer quartiles).
- DuPont decomposition of ROE.
- Scenario & sensitivity (revenue, COGS, WACC).
- Export `reports/Executive_Summary.pdf` (1–2 pages).
- (Optional) add `model-view.png` with relationships.

---

## Conventions / decisions
- No theme file in the repo (README does not include an “Apply theme” step).
- Deneb JSON: clean JSON (no `//` or `/* ... */` comments).
- Status palette via `palette` table; status buckets: `below / at_norm / above`.
- All labels and documentation are in **English**.

---

## Housekeeping
- Social preview (optional): Settings → General → Social preview — you can use `/assets/dashboard_cover.png`.
- If GitHub Pages caches images, append a version query (e.g., `?v=1`) to force refresh.
