# marketing-intelligence-engine
End-to-end marketing analytics engine on Snowflake covering  funnel analysis, CLV, time-decay attribution, lead velocity,  channel saturation and anomaly alerting across 11 mart tables.

# ❄️ Snowflake Marketing Intelligence Engine

## What is this?
Marketing analytics pipeline built entirely 
on Snowflake that transforms raw campaign, lead, and conversion 
data into actionable business intelligence across 11 analytical 
models.

The pipeline answers the questions every B2B SaaS marketing and 
revenue team cares about:
- Which channels drive the highest ROI and lowest CAC?
- Where are leads dropping off in the funnel?
- Which customers will generate the most lifetime value?
- Are we seeing diminishing returns on any channel?
- Is our pipeline accelerating or slowing down?
- Which touchpoint actually deserves credit for a conversion?

## Architecture
RAW → STAGING → MART → MONITORING

## Metrics & Models

### 🔵 Funnel Intelligence
- **Channel Performance** — ROI, CPL, conversion rate per channel
- **Funnel Drop-off Analysis** — where leads are lost, ranked by channel
- **Campaign ROI Summary** — net profit, ROI multiplier, budget share

### 🟢 Lead Intelligence  
- **Lead Quality Scoring** — weighted model scoring each lead on 
  industry fit, geography, plan type and deal value (0–100 score, 
  A/B/C/D grading)
- **Lead Velocity Rate** — MoM pipeline momentum with 3-month 
  rolling average and acceleration signals per channel

### 🟡 Attribution Intelligence
- **Multi-touch Attribution** — First Touch, Last Touch, Linear 
  and U-shaped models compared side by side
- **Time Decay Attribution** — exponential half-life model 
  (7-day decay) giving more credit to touchpoints closer 
  to conversion

### 🟠 Revenue Intelligence
- **Customer Lifetime Value** — predicted CLV using churn rate, 
  contract length and expansion multiplier per industry; 
  CLV:CAC health scoring (Excellent / Healthy / Marginal / 
  Unprofitable)
- **Cohort Analysis** — leads grouped by acquisition month 
  tracking conversion rate, revenue and avg months to convert 
  with cumulative revenue window

### 🔴 Risk Intelligence
- **Channel Saturation & Diminishing Returns** — detects when 
  spend is increasing but ROI is falling using LAG comparisons 
  and efficiency scoring
- **Marketing Anomaly Alerts** — flags channels with ROI below 
  2x or lead spikes above 150% of average in real time

## SQL Concepts Demonstrated
| Concept | Used In |
|---|---|
| Window Functions (RANK, DENSE_RANK) | Funnel, CLV, Attribution |
| LAG / LEAD | Saturation, Velocity |
| FIRST_VALUE / LAST_VALUE | Attribution |
| ROWS BETWEEN custom frames | Velocity rolling avg |
| POWER() exponential decay | Time Decay Attribution |
| Multi-CTE chaining | CLV, Cohort, Saturation |
| NULLIF divide-by-zero guard | All mart tables |
| Weighted scoring models | Lead Quality |
| LEFT JOIN preservation | All channel metrics |
| CASE WHEN business logic | Alerts, Grading, Signals |

## How to Run
1. Execute scripts in folder order 01 → 05
2. All scripts use CREATE OR REPLACE — safe to re-run anytime
3. Start with RAW → STAGING → MART → MONITORING → ADVANCED

## Stack
- **Warehouse** — Snowflake (free tier compatible)
- **Language** — Pure SQL
- **Pattern** — RAW / STAGING / MART (dbt-style layering)
