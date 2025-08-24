# Methodology

This document explains the **data model, calculation logic, norm rules, and visual conventions** used in the Power BI report.

- Back to project overview: **[README](../README.md)**

---

## 1) Data model

**Tables**

- **financials_long** — fact table (yearly values in long format).  
  Columns include `Year`, `Statement` (Assets, Equity, Revenue, etc.), `Value`, and base/index helpers.
- **ratios** — measure table hosting KPI measures and helpers (YoY, norm status, colors).
- **years** — helper dimension for year filtering and Latest/Base logic.
- **palette** — color hexes for status categories and legend dots.
- **Sections** — small helper table for page-level slicers/labels.

**Relationships**

- Star-style around `financials_long[Year]` (many-to-one to `years[Year]`).
- No page-specific fields; **both pages** read from the **same model**.

---

## 2) Calculation logic

### 2.1 Base / Latest years
- **Latest Year** = max available year within current filter context.  
- **Base Year** = comparison year (usually `Latest − 1`) or a pinned year for indexed visuals.

### 2.2 YoY deltas
- **YoY Δ** = `Value(Latest) − Value(Prev)`  
- **YoY Δ %** = `DIVIDE(Value(Latest) − Value(Prev), Value(Prev))`  
- Arrow sign:
  - ▲ if Δ > 0
  - ▼ if Δ < 0
  - ● if Δ = 0 or previous is blank
- Defensive blanks: when `Value(Prev)` is blank/zero, percent delta is suppressed and the chip shows “–”.

### 2.3 Indexed trends
- **Index** (e.g., Assets/Equity/Revenue) = `Value / Value(Base Year)` → displayed as 100 at the base.

---

## 3) Norms & flags

Each KPI has a **soft band** with a neutral zone. Norm bands are set in the model and reflected in visuals.

- Inputs per KPI:
  - `Norm Low`, `Norm High`
  - `better_is` ∈ {`higher`, `lower`}
- **Status buckets**:
  - `below` — value < `Norm Low`
  - `at_norm` — `Norm Low` ≤ value ≤ `Norm High`
  - `above` — value > `Norm High`
- **Directionality**:
  - If `better_is = higher`, moving upward is good.
  - If `better_is = lower`, moving downward is good.
- **Color mapping**: status → hex color via the `palette` table.  
  The same mapping drives badges, legend dots, and bars.

---

## 4) Formatting conventions

- **DAX style**: comma-separated arguments; consistent naming `grp__KPI__SubKPI__MeasureName`.
- **Number formatting**:
  - Percent KPIs show `%` with sensible decimals (context-driven).
  - Absolute KPIs use compact format (e.g., `1.2M` when appropriate).
- **Tooltips**: show YoY absolute and percent deltas alongside the current value.
- **Defensive rules**: use `DIVIDE`; empty states render “–”.

---

## 5) Visual layer

### 5.1 Deneb (Vega-Lite)
Reproducible JSON specs (no comments) are stored under **`/deneb`**:

- `kpi_bars_numeric.vl.json` — bars for absolute-value KPIs  
- `kpi_bars_percent.vl.json` — bars for percent KPIs  
- `legend_status.vl.json` — compact legend using palette/status  
- `row_labels.vl.json` — left-aligned KPI labels  
- `trend_indexed.vl.json` — small multiple indexed trends  
- `trend_pnl.vl.json` — revenue / EBIT / net profit trends

> Specs are clean JSON and parameterised via fields/measures; styling stays minimal to keep portability between pages.

### 5.2 Per-KPI trend badge (native Card)
- **Direction:** ▲ / ▼ / ● from `YoY Δ`
- **Color:** derived from current **Norm Status** (status → hex)
- **Chip text:** formatted label (`▲ +2.1` or `▼ −13%`)
- **Blank rule:** hide when previous year is missing

---

## 6) Visual design — two-page setup

Both dashboard pages use the **same data and measures**; only the visual styling differs so we can serve two purposes: a sleek on-screen view and clean screenshots for the Word report.

| Variant | Intent | Where to use |
|---|---|---|
| **v1 — rounded cards (site style)** | Web/presentation look with soft background and a title divider | On-screen portfolio and overview |
| **v2 — flat cards (print-friendly)** | Neutral, “flat” visuals that paste cleanly into Word | Screenshots for Word section **3.2** |

### 6.1 Styling spec — v1 (rounded cards)
- **Card background:** `#E0E2E1`  
- **Border:** `#C7CCCA`, **width:** `1 px`  
- **Corner radius:** `12 px`  
- **Shadow:** `#BDC2C0` (subtle)  
- **Title separator (line):** `#BDC2C0`, **thickness:** `1 px`  
- **Inner padding:** `top 10 px · right 18 px · bottom 10 px · left 8–12 px`  
- **Note:** Optimised for web; visuals keep compact `top` padding (~`4`).

### 6.2 Styling spec — v2 (flat cards, print-friendly)
- **Border:** `#B8BEC3`  
- **Corner radius:** `0` (no rounding)  
- **Shadow:** none  
- **Title separator:** none  
- **Background:** none  
- **Inner padding:** comfortable margins for cropping in Word  
- **Visual padding (`top`):** `15` (updated in each visual’s JSON; was `4`)  
- **Rationale:** flat, neutral skin avoids clashes with Word page background and table rules.

### 6.3 Why this matters
- **Readability in Word.** No shadows/rounding/separators; borders align with document rules.  
- **Consistent crops.** Extra top padding prevents clipping of titles/legends.  
- **Traceability.** Because both pages share measures, any data update appears in both variants identically.

### 6.4 Files & locations
Gallery screenshots used on the live page:

- [`cover.png`](./cover.png) — v1 (rounded)  
- [`cover2.png`](./cover2.png) — v2 (flat)

---

## 7) Reproducibility checklist

- Versioned measures in **`/dax`**  
- Deneb JSON specs in **`/deneb`**  
- Anonymised sample data in **`/data`**
