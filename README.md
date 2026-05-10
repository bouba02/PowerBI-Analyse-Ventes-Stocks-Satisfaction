# VéloSahel — Sales, Inventory & Customer Satisfaction Dashboard | Power BI

> **Bicycle & accessories distribution · West Africa**  
> 3 performance axes · Dynamic stock alerts · Star Schema · 54-min YouTube demo

🇫🇷 [Version française disponible ici](README_FR.md)

---

## Business Problem

A bicycle and accessories distributor operating across West Africa was managing
its operations from scattered Excel files — no consolidated view on sales performance,
critical stock levels, or customer satisfaction trends.

**3 unanswered questions for management:**

| Axis | Question |
|---|---|
| Sales | What is the performance by product, period, and client? |
| Inventory | Which products are critically out of stock or overstocked? |
| Satisfaction | How is the customer rating evolving and what early signals to detect? |

**Mission:** Centralize operational management in a single tool — updatable,
readable by management, with automated alerts on stock-outs.

---

## Dashboard — 2 Views

| Management View | Stock Alerts |
|:-:|:-:|
| ![Direction](Direction.png) | ![Stock Alert](Alerte%20Stock%24.png) |

**Management View:** Commercial performance by product category · Revenue trends ·
Top products · Customer satisfaction evolution · Executive KPI summary

**Stock Alerts View:** Products below critical threshold · Recommended reorder
frequencies · Dynamic color-coded alerts by risk level

---

## Full Demo

[![Watch on YouTube](https://img.youtube.com/vi/VAYAVpYkcMg/maxresdefault.jpg)](https://youtu.be/VAYAVpYkcMg)

▶️ **[Full walkthrough — 54 minutes](https://youtu.be/VAYAVpYkcMg)**

---

## Data Model — Star Schema

```
[Inventory]     [Customer Reviews]
      └──────────────┘
              │
          [Sales]          ← Fact table
              │
         [Calendar]        ← DAX date table
```

**3 consolidated sources:** `Ventes.csv` · `Inventaire.csv` · `Avis-Clients.csv`

---

## DAX Measures

| Measure | Description |
|---|---|
| `Total_Revenue` | Global revenue and by product category |
| `Units_Sold` | Volume — global, by product, by period |
| `Avg_Satisfaction_Score` | Weighted by transaction volume |
| `Stockout_Rate` | % products below defined alert threshold |
| `Conditional_Alerts` | Visual indicators based on business thresholds |

**Stock alert logic:**
```dax
Stock_Alert =
VAR CurrentStock = [Current_Stock]
VAR AlertThreshold = [Reorder_Point]
RETURN
SWITCH(TRUE(),
    CurrentStock = 0,                  "Critical stockout",
    CurrentStock <= AlertThreshold,    "Urgent reorder",
    CurrentStock <= AlertThreshold*2,  "Monitor stock",
    "Stock OK"
)
```

---

## Recommendations Delivered to Management

- Critical stockout products identified with calculated reorder frequencies
- Product categories ranked by revenue performance and trend (up / down / stable)
- Customer satisfaction early warnings — categories below acceptable score threshold
- Business rules fully documented for maintainable use by the internal team

---

## Tech Stack

- **Power BI Desktop** — report, visualizations, multi-page navigation
- **Power Query / M** — cleaning, transformation, consolidation of 3 CSV sources
- **DAX** — calculated measures, KPIs, time intelligence
- **Star Schema** — optimized relational modeling

---

## Quick Start

```bash
git clone https://github.com/bouba02/PowerBI-Analyse-Ventes-Stocks-Satisfaction.git
```

Open `SahelVelo Dashboard.pbix` in Power BI Desktop.  
If sources don't load: `Home → Transform Data → Data Source Settings` → redirect to the CSV files in the cloned folder.

---

## Repository Structure

```
VeloSahel/
├── README.md
├── README_FR.md
├── SahelVelo Dashboard.pbix
├── SahelVelo Dashboard.pdf
├── Ventes.csv
├── Inventaire.csv
├── Avis-Clients.csv
├── Direction.png
└── Alerte Stock.png
```

---

## Author

**Boubacar Nikiema** — Data Analyst & BI Consultant

Specialized in operational dashboards, Sales & Supply Chain analytics and performance
management using Power BI, SQL, Python and Excel. Based in Morocco, working with
clients across Africa and French-speaking Europe.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-boubacar--nikiema-blue?logo=linkedin)](https://linkedin.com/in/boubacar-nikiema)
[![YouTube](https://img.shields.io/badge/YouTube-BoubacarDataAnalyst-red?logo=youtube)](https://youtube.com/@BoubacarDataAnalyst)
[![Email](https://img.shields.io/badge/Email-nikiemaboubacar%40gmail.com-gray?logo=gmail)](mailto:nikiemaboubacar@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-data.ngroupmediadigital.com-green)](https://data.ngroupmediadigital.com)

---

*Simulated data · Code: MIT License*
