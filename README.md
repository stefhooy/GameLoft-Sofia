# Gameloft Sofia — Data Analyst Test

**Candidate:** Stephan Pentchev
**Role:** Data Analyst

---

## Overview

This repository contains the full solution to the Gameloft Sofia Data Analyst take-home assessment. The work is split into two parts:

- **Part 1 — Event EDA:** Churn and revenue analysis of a live game event using Python and Power BI
- **Part 2 — A/B Test Analysis:** Interpretation of an A/B test with conflicting ARPDAU and ARPPU signals

---

## Repository Structure

```
.
├── Test for Data Analyst.pdf                 # Original test brief
├── Event_Performance_Review.pdf              # Final presentation deck
├── Gameloft_Sofia_Event_Visualizations.pbix  # Power BI dashboard
└── Part_2_EDA/
    ├── Game Event Analysis.ipynb         # Full Python analysis (Parts 1 & 2)
    ├── Test Data analyst.xlsx            # Raw event data
    ├── part1_powerbi_tables.xlsx         # Cleaned tables exported for Power BI
    ├── churn_top10_dropout.png           # Q1a: Top 10 missions by players lost
    ├── churn_top10_rate.png              # Q1a: Top 10 missions by churn rate
    ├── churn_heatmap_levelgroup.png      # Q1b: Churn rate heatmap by level group × chapter
    ├── revenue_by_levelgroup.png         # Q2b: Revenue and skip rate by level group
    ├── revenue_top15_missions.png        # Top 15 missions by revenue
    └── recommendations_impact.png        # Expected impact of 4 recommendations
```

---

## Part 1 — Game Event Analysis

**Data:** 2,040 rows — one per (player level × mission), covering levels 2–41 across 5 chapters and 51 missions.

**Revenue model:** Players pay premium currency to skip missions. 100 gems = $4.99 → 1 gem = $0.0499.

### Questions answered

| # | Question | Key finding |
|---|----------|-------------|
| **1a** | Which missions lose the most players? | Chapter 1 missions 1–4 cause the largest absolute dropout (~1.1M players combined). Chapter 5 Mission 16 has the highest churn *rate* (~71%). |
| **1b** | Does churn differ by player level? | Yes — early-game players (Lvl 2–11) show the highest absolute churn. Churn rate patterns vary significantly across chapters and level groups (see heatmap). |
| **1c** | Total event revenue? | **$224,111.38** from 154,353 skips across 12.1M mission starts (1.27% overall skip rate). |
| **1d** | Which level groups generated the most revenue? | Lvl 2–11 contributes ~48% of revenue due to volume. High-level players (Lvl 32–41) have a higher skip rate despite smaller numbers. |
| **2** | Recommendations? | 4 recommendations with quantified expected impact — see below. |

### Recommendations & Expected Revenue Impact

| Recommendation | Estimated Uplift |
|---|---|
| Fix Chapter 1 funnel (10% retention improvement) | +$14,794 |
| Rescue Chapter 5 cliff — reward before Mission 17 (50% recovery) | +$33,768 |
| Introduce 75-gem skip tier in top Chapter 2 missions | +$38,076 |
| Discounted first-skip offer for Lvl 2–11 players | +$97,995 |
| **Total projected uplift** | **+$184,634** |

---

## Part 2 — A/B Test Analysis

**Test results:**

| Metric | Group A (Control) | Group B (Treatment) | Δ |
|--------|:-----------------:|:-------------------:|:--:|
| ARPDAU | $0.15 | $0.16 | +6.7% |
| ARPPU | $30.00 | $16.00 | −46.7% |

**Q1 — Which group wins?** Group B (provisionally). ARPDAU is the stronger business signal as it reflects monetization across the full player base. The +6.7% lift is directionally positive, pending a significance test.

**Q2 — Why do the metrics diverge?** Group B likely attracted more players into spending at lower amounts. More payers at lower spend → ARPDAU up, ARPPU down. Group A has fewer but higher-value ("whale") payers.

**Q3 — What feature was likely tested?** A low-cost entry-level offer — e.g. a starter pack, discounted currency bundle, or reduced-price skip — that lowered the spending barrier for new payers. This is the textbook mechanism for this exact ARPDAU/ARPPU divergence pattern.

**Before declaring a final winner:** statistical significance, sample size, test duration, retention impact, and payer rate comparisons are all required.

---

## How to Run the Notebook

1. Install dependencies: `pip install pandas numpy matplotlib seaborn openpyxl`
2. Open `Part_2_EDA/Game Event Analysis.ipynb` in Jupyter
3. Ensure `Test Data analyst.xlsx` is in the same folder
4. Run all cells — charts and Excel exports are generated automatically

---

## Tools Used

- **Python** (pandas, numpy, matplotlib, seaborn) — data processing and charting
- **Power BI** — interactive dashboard (`Gameloft_Sofia_Event_Visualizations.pbix`)
- **PowerPoint** — executive summary presentation
