# DAX measures

This folder contains the full list of measures exported from the Power BI model.

- **File:** `measures.dax` (read-only listing for reviewers)
- **Scope:** all KPIs used across the dashboard (liquidity, capital structure/solvency, profitability, structure & trends)
- **Palette logic:** statuses `below / at_norm / above` are mapped to HEX from the `palette` table

## What to look for

**Norm bands & color**
- `Norm Low`, `Norm High` – thresholds per KPI (sourced from `ratio_norms`)
- `Ratio Value` – value of the current KPI in context
- `Norm Status` – returns `below / at_norm / above`
- `Color Hex` – looks up the HEX color by status

**Trends & deltas**
- `Delta vs Base`, `Indexed %`, `YoY Δ / YoY Delta`, chip/arrow helpers
- Base and index measures for Assets, Equity, Revenue

**Business KPIs**
- Liquidity: Cash ratio, Current ratio, Quick ratio, Months to repay
- Capital structure & solvency: Equity ratio, Debt to equity, Working capital, Altman index
- Profitability & returns: ROA, ROE, Net profit margin, EBITDA margin

> The full source is in `measures.dax`. README shows only the overview to keep the repo browsable.

## How this file is generated

Use one of the options below whenever the model changes.

### A) Tabular Editor 2 (script; recommended)
1. Open PBIX → **External Tools → Tabular Editor** → tab **C# Script**.  
2. Run the script below (adjust the path if needed). It creates `measures.dax`.

```csharp
// Export all measures to C:\Projects\measures.dax
var path = @"C:\Projects\measures.dax";
var sb = new System.Text.StringBuilder();
foreach (var m in Model.AllMeasures.OrderBy(x => x.Table.Name).ThenBy(x => x.Name))
{
    sb.AppendLine("-- " + m.Table.Name + "[" + m.Name + "]");
    sb.AppendLine(m.Name + " = " + m.Expression);
    sb.AppendLine();
}
System.IO.File.WriteAllText(path, sb.ToString(), System.Text.Encoding.UTF8);
