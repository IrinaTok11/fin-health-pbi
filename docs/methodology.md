## Visual design — two-page setup

Both dashboard pages use the **same data and measures**; only the visual styling differs so we can serve two purposes: a sleek on-screen view and clean screenshots for the Word report.

| Variant | Intent | Where to use |
|---|---|---|
| **v1 — rounded cards (site style)** | Web/presentation look with soft background and a title divider | On-screen portfolio and overview |
| **v2 — flat cards (print-friendly)** | Neutral, “flat” visuals that paste cleanly into Word | Screenshots for Word section **3.2** |

### Styling spec — v1 (rounded cards)
- **Card background:** `#E0E2E1`  
- **Border:** `#C7CCCA`, **width:** `1 px`  
- **Corner radius:** `12 px`  
- **Shadow:** `#BDC2C0` (subtle)  
- **Title separator (line):** `#BDC2C0`, **thickness:** `1 px`  
- **Inner padding:** `top 10 px · right 18 px · bottom 10 px · left 8–12 px`  
- **Note:** Optimised for web; visuals keep compact `top` padding (~`4`).

### Styling spec — v2 (flat cards, print-friendly)
- **Border:** `#B8BEC3`  
- **Corner radius:** `0` (no rounding)  
- **Shadow:** none  
- **Title separator:** none  
- **Background:** none  
- **Inner padding:** comfortable margins for cropping in Word  
- **Visual padding (`top`):** `15` (updated in each visual’s JSON; was `4`)  
- **Rationale:** flat, neutral skin avoids clashes with Word page background and table rules.

### Why this matters
- **Readability in Word.** No shadows/rounding/separators; borders align with document rules.  
- **Consistent crops.** Extra top padding prevents clipping of titles/legends.  
- **Traceability.** Because both pages share measures, any data update appears in both variants identically.

### Files & locations
- Gallery screenshots used on the live page:  
  - `docs/assets/dashboard_cover.png` — v1 (rounded)  
  - `docs/assets/dashboard_cover2.png` — v2 (flat)
