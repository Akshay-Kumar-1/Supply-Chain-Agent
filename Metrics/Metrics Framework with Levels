# SupplyChain Agent — Metrics

> **A comprehensive, three-stage metrics framework for AI-powered supply chain agents.**  
> Covers the full journey: from the pain state (before), through the build (during), to production (after).

---

## Table of Contents

- [Level Definitions](#level-definitions)
- [Stage 1: Before the Agent — The Pain State](#stage-1-before-the-agent--the-pain-state)
  - [Business & Financial — Before](#business--financial--before)
  - [Technical — Before](#technical--before)
  - [Supply Chain & Operations — Before](#supply-chain--operations--before)
- [Stage 2: During Build — AI / ML / Agent Metrics](#stage-2-during-build--ai--ml--agent-metrics)
  - [Business & Financial — During Build](#business--financial--during-build)
  - [Technical / AI / ML / Agent — During Build](#technical--ai--ml--agent--during-build)
  - [Supply Chain & Operations — During Build](#supply-chain--operations--during-build)
- [Stage 3: Production — New Metrics Unlocked by the Agent](#stage-3-production--new-metrics-unlocked-by-the-agent)
  - [Business & Financial — Production](#business--financial--production)
  - [Technical — Production](#technical--production)
  - [Supply Chain & Operations — Production](#supply-chain--operations--production)
- [Master Summary: Metrics by Level Across All Stages](#master-summary-metrics-by-level-across-all-stages)
  - [Count Summary](#count-summary)
  - [How Levels Connect: The Diagnostic Cascade](#how-levels-connect-the-diagnostic-cascade)
  - [Persona → Level Mapping](#persona--level-mapping)

---

## Level Definitions

The framework uses three levels to classify every metric:

```
L1 — SURFACE METRICS (What happened?)
  • Lagging indicators, easy to observe
  • Typically on executive dashboards
  • Tell you the outcome but NOT why
  • Examples: Revenue, stockout count, total cost
  • Audience: VP/C-Suite, board, investors

L2 — DIAGNOSTIC METRICS (Why did it happen?)
  • Leading + lagging mix, require some analysis
  • Connect cause to effect
  • Tell you WHERE the problem is and what's driving L1
  • Examples: Forecast accuracy, supplier on-time rate, days of stock
  • Audience: Supply Chain Manager, Procurement Lead, Logistics Coordinator

L3 — DEEP / ROOT CAUSE METRICS (How do we fix it?)
  • Leading indicators, granular, often per-SKU or per-supplier
  • Require deep analysis or AI to surface
  • Tell you the SPECIFIC lever to pull to improve L2, which improves L1
  • Examples: Lead time variability, demand CV per SKU, prompt token efficiency
  • Audience: Analysts, engineers, domain experts, the AI agent itself
```

**Relationship: L3 drives → L2 drives → L1**  
If L1 is bad, dig into L2 to diagnose, then into L3 to find the fix.

---

## Stage 1: Before the Agent — The Pain State

### Business & Financial — Before

#### L1 — Surface (Outcome Metrics)

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Stockout Revenue Loss | ₹ revenue lost because products were unavailable | NOT TRACKED | VP Ops | No one connects stockouts to ₹ lost — it's invisible P&L leakage |
| 🟡 Total Inventory Value | ₹ capital tied up in warehouse stock | PARTIALLY | VP Ops / CFO | Known from balance sheet but not optimized — treated as fixed cost |
| 🟡 Total Procurement Spend | ₹ spent on purchasing goods and materials | PARTIALLY | VP Ops | Finance knows the total but no one analyzes where the waste is |
| 🔴 Gross Margin Erosion from SC | % of margin lost to SC inefficiency (rush buys, write-offs, waste) | NOT TRACKED | VP Ops | Finance sees margin compression but can't attribute it to supply chain |
| 🟡 Freight / Logistics Spend | Total ₹ spent on shipping and transportation | PARTIALLY | VP Ops | Known as a line item — never broken down or optimized |

#### L2 — Diagnostic (Driver Metrics)

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Inventory Carrying Cost (%) | Annual cost of holding inventory as % of inventory value (storage, insurance, depreciation, capital cost) | NOT TRACKED | SCM / VP Ops | No one calculates beyond rent — opportunity cost of capital ignored |
| 🔴 Emergency Procurement Premium | Extra ₹ paid on rush/spot purchases vs. contract price | NOT TRACKED | Procurement | Invoices are paid individually — no one aggregates the premium pattern |
| 🔴 Dead Stock Value | ₹ value of inventory with zero sales in 60+ days | NOT TRACKED | SCM | Only discovered during annual physical audit — months too late |
| 🔴 Maverick Spend % | % of purchases made outside preferred supplier contracts | NOT TRACKED | Procurement | Individual buyers make spot decisions — no visibility into compliance |
| 🔴 Cash-to-Cash Cycle Time | Days between paying suppliers and receiving customer payment (DIO + DSO - DPO) | NOT TRACKED by SC team | VP Ops | Finance tracks it loosely — SC team has zero visibility into their impact |
| 🔴 Customer Churn from Stockouts | Customers lost because of repeated unavailability | NOT TRACKED | VP Ops | No root cause analysis linking churn to fulfillment failures |

#### L3 — Deep / Root Cause

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Cost per Stockout Event | Average ₹ impact of a single stockout (lost sale + customer goodwill + rush reorder cost) | NOT TRACKED | SCM | Can't even count stockouts reliably, let alone cost them |
| 🔴 TCO per Supplier | True total cost including price + freight + defects + delays + admin overhead | NOT TRACKED | Procurement | Data scattered across invoices, emails, QC reports — no one aggregates |
| 🔴 Working Capital Efficiency Ratio | Revenue generated per ₹ of inventory held | NOT TRACKED | VP Ops / CFO | Requires connecting sales velocity to stock levels per SKU — too manual |
| 🔴 Carrying Cost per SKU Category | Which product categories cost the most to hold relative to their revenue? | NOT TRACKED | SCM | Requires SKU-level inventory cost allocation — not done |
| 🔴 Freight Cost per Unit per Route | Shipping cost broken down by product, route, and carrier | NOT TRACKED | Logistics | Total freight known, unit-level breakdown not calculated |

---

### Technical — Before

#### L1 — Surface

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Manual Process Hours / Week | Total hours team spends on repetitive SC tasks | NOT TRACKED | SCM | Everyone is "busy" but no one quantifies HOW the time is spent |
| 🔴 Number of Data Silos | Count of disconnected systems/files holding SC data | NOT TRACKED | SCM | No one audits their own data architecture — it just grows organically |
| 🟡 Report Generation Time | Hours to produce weekly/monthly SC report | INFORMALLY KNOWN | SCM | "It takes me all of Monday morning" — known but not formally measured |

#### L2 — Diagnostic

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Data Freshness | Average age of data used for decisions (hours/days) | NOT TRACKED | SCM | No one measures — but inventory data is typically 2-7 days stale |
| 🔴 Data Consistency Score | Do different team members have the same numbers? | NOT TRACKED | SCM | S&OP meetings start with "whose numbers are right?" — no single source of truth |
| 🔴 Decision Cycle Time | Hours/days from "problem detected" to "action taken" | NOT TRACKED | SCM | Stockout → PO: 1-3 days. Supplier issue → action: 1-2 weeks. Nobody measures this |
| 🔴 Error Rate in Manual Processes | % of POs, reports, or entries containing errors | NOT TRACKED | Procurement | Errors discovered ad-hoc when suppliers receive wrong quantities |

#### L3 — Deep / Root Cause

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Data Completeness % | What percentage of required fields are actually filled in Excel files? | NOT TRACKED | All | Blank cells, missing dates, inconsistent formats — no audit |
| 🔴 Reconciliation Time per Data Source | Hours spent matching data across systems | NOT TRACKED | SCM | Buried inside "report preparation time" — not isolated |
| 🔴 Process Bottleneck Identification | Which manual step takes the most time or causes most errors? | NOT TRACKED | All | No process instrumentation — everything is a black box |

---

### Supply Chain & Operations — Before

#### L1 — Surface

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🟡 Fill Rate / Service Level | % of customer orders fulfilled completely from stock | POORLY TRACKED | SCM / VP Ops | Known qualitatively ("about 90%") — not per SKU, not trended |
| 🟡 Inventory Turnover Ratio | COGS / Average Inventory — how fast stock moves | PARTIALLY (aggregate) | VP Ops | Finance knows the number. SC team doesn't track it per SKU or category |
| 🔴 Stockout Frequency | Count of SKU-location combinations hitting zero stock | NOT TRACKED proactively | SCM | Discovered when customer order fails — reactive counting only |
| 🟡 On-Time Delivery to Customer | % of outbound shipments arriving in promised window | PARTIALLY | Logistics | Tracked from complaints, not systematically across all shipments |
| 🔴 Supply Chain Health Score | Single composite metric summarizing overall SC performance | DOES NOT EXIST | VP Ops | No framework to create one — would require aggregating 20+ data points |

#### L2 — Diagnostic

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Days of Inventory (DOI) per SKU | How many days current stock will last at current demand | NOT TRACKED | SCM | The #1 metric for preventing stockouts — and most SMBs don't know it |
| 🔴 Forecast Accuracy (MAPE) | How close demand predictions are to actual demand | NOT TRACKED | SCM | No formal forecast exists — it's gut-feel or basic Excel average |
| 🔴 Supplier On-Time Delivery Rate | % of supplier deliveries arriving by promised date | NOT TRACKED systematically | Procurement | Known anecdotally ("Supplier X is always late") but not measured |
| 🔴 Supplier Quality / Defect Rate | % of received goods failing quality inspection | PARTIALLY (paper) | Procurement | Paper records or disconnected spreadsheet — not linked to supplier scoring |
| 🔴 Shipment Exception Rate | % of shipments experiencing delays, damage, or loss | NOT AGGREGATED | Logistics | Each exception handled ad-hoc — no one knows the total rate |
| 🔴 Overstock Ratio | % of SKUs where stock exceeds 3× monthly demand | NOT TRACKED | SCM | Overstock sits silently — only found during physical audit |
| 🔴 Risk Exposure Score | Quantified risk from supplier concentration, geography, etc. | DOES NOT EXIST | VP Ops / SCM | No risk quantification of any kind |

#### L3 — Deep / Root Cause

| Metric | Definition | Tracked? | Persona | Why Stuck |
|--------|-----------|:--------:|---------|-----------| 
| 🔴 Demand Variability (CV per SKU) | Coefficient of variation — how volatile each SKU's demand is | NOT TRACKED | SCM | All SKUs treated the same — stable staples managed like volatile seasonal items |
| 🔴 Forecast Bias | Systematic tendency to over- or under-forecast | NOT TRACKED | SCM | No forecast → no bias measurement → chronic over-ordering "just in case" |
| 🔴 Supplier Lead Time Variability | Standard deviation of actual vs. promised lead times | NOT TRACKED | Procurement / SCM | Single "average lead time" used that may be months old — variability ignored |
| 🔴 Supplier Concentration Risk | % of SKUs or spend dependent on a single supplier | NOT TRACKED | SCM | 30-60% of SMBs have critical single-source dependencies they don't know about |
| 🔴 Safety Stock Calibration | Is current safety stock appropriate for demand variability and lead time? | NOT DONE | SCM | Safety stock set by gut-feel once and never adjusted |
| 🔴 Time to Detect Disruption | Hours/days between a disruption occurring and team knowing | NOT TRACKED | SCM | Usually 2-7 days — by which time the damage is done |
| 🔴 Time to Recover from Disruption | Days from detection to operations returning to normal | NOT TRACKED | SCM / VP Ops | Each disruption handled as unique crisis — no measurement, no playbook |
| 🔴 Carrier Performance by Route | Which carrier performs best on which route? | NOT TRACKED | Logistics | Carrier selection is habitual, not data-driven |
| 🔴 Contract Compliance Rate | % of purchases at contracted terms vs. spot/off-contract | NOT TRACKED | Procurement | Contracts exist in PDFs — no one monitors compliance |
| 🔴 Inter-Warehouse Imbalance | SKUs where one warehouse is overstocked while another is out | NOT DETECTED | SCM | Each warehouse managed in isolation — network view doesn't exist |

---

## Stage 2: During Build — AI / ML / Agent Metrics

### Business & Financial — During Build

#### L1 — Surface

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| Build Completion % | L1 | MVP | Overall progress: workflows built / total planned | 7/7 by Week 5 |
| Total Build Cost | L1 | MVP | All development costs (labor + tools + API) | < $10,000 |
| Beta Users Onboarded | L1 | Beta | Active users with running setup | 8-10 |
| Stated WTP (Willingness to Pay) | L1 | Beta | Price users say they'd pay in interviews | > $200/month |

#### L2 — Diagnostic

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| Sprint Completion Rate | L2 | MVP | % of planned sprint tasks completed | > 80% |
| Time per Workflow Build | L2 | MVP | Hours to build and test each agent module | < 15 hrs each |
| Activation Rate | L2 | Beta | % of invited users who complete full setup | > 80% |
| Time to First Value | L2 | Beta | Hours from invite to user receiving first useful output | < 24 hours |
| LLM API Cost per Day (dev) | L2 | MVP | Daily spend on Claude during development/testing | < $5/day |
| Projected Cost per User per Month | L2 | Beta | (Total infra + API cost) / active users projected | < $15 |

#### L3 — Deep / Root Cause

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| Cost per LLM Call | L3 | MVP → Beta | Average $ per individual Claude API request | < $0.015 |
| Token Efficiency per Call | L3 | MVP | Avg tokens (prompt + response) — optimize to reduce cost | Minimize while maintaining quality |
| Onboarding Drop-Off Point | L3 | Beta | Exact step where users abandon setup | Identify and fix |
| Beta User Engagement Depth | L3 | Beta | Which briefing sections users read vs. skip | Identify low-value sections |

---

### Technical / AI / ML / Agent — During Build

#### L1 — Surface (System Health)

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| Workflow Execution Success Rate | L1 | MVP → Beta | % of workflow runs completing without error | > 90% (dev) → > 95% (beta) |
| Full Pipeline Completion | L1 | Beta | Does the daily 7-workflow pipeline finish every day? | > 95% of days |
| LLM Response Availability | L1 | MVP → Beta | % of API calls that return a valid response | > 99% |
| End-to-End Pipeline Time | L1 | Beta | Total minutes for all 7 workflows to complete | < 45 minutes |

#### L2 — Diagnostic (Agent Quality)

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| JSON Parse Success Rate | L2 | MVP | % of LLM responses that are valid parseable JSON | > 95% |
| Schema Compliance Rate | L2 | MVP | % of responses matching expected output structure | > 90% |
| Hallucination Rate | L2 | MVP → Beta | % of outputs containing fabricated data | < 5% |
| User-Validated Accuracy | L2 | Beta | % of agent recommendations users agree with | > 70% |
| False Positive Alert Rate | L2 | Beta | % of alerts users dismiss as irrelevant | < 20% |
| PO Approval Rate (no modifications) | L2 | Beta | % of auto-generated POs approved as-is | > 60% |
| Briefing Open Rate | L2 | Beta | % of daily briefing emails opened | > 60% |
| Alert Action Rate | L2 | Beta | % of critical alerts acted on within 4 hours | > 50% |
| Reasoning Quality Score | L2 | MVP | Human expert rating of LLM analysis quality (1-5) | > 3.5/5 |

#### L2 — Per-Agent Quality Metrics

| Agent | Metric | Level | Beta Target | Prod Target |
|-------|--------|:-----:|:-----------:|:-----------:|
| **Demand** | MAPE (forecast accuracy) | L2 | < 30% | < 20% |
| **Demand** | Anomaly Detection Precision | L2 | > 60% | > 75% |
| **Demand** | Directional Accuracy (trend up/down/flat) | L2 | > 70% | > 80% |
| **Inventory** | Classification Accuracy (Crit/Low/Healthy/Over) | L2 | > 85% | > 95% |
| **Inventory** | Reorder Recommendation Acceptance Rate | L2 | > 60% | > 80% |
| **Supplier** | Score-to-Reality Correlation | L2 | > 0.5 | > 0.7 |
| **Supplier** | Risk Flag Accuracy | L2 | > 50% | > 70% |
| **Logistics** | Delay Prediction Accuracy | L2 | > 55% | > 75% |
| **Logistics** | False Alarm Rate (delays) | L2 | < 30% | < 15% |
| **Risk** | Risk Detection Recall | L2 | > 40% | > 65% |
| **Risk** | Risk Relevance Precision | L2 | > 50% | > 70% |
| **Risk** | Detection Lead Time | L2 | > 1 day | > 3 days |
| **Procurement** | PO Auto-Generation Accuracy | L2 | > 70% | > 90% |
| **Procurement** | Supplier Selection Agreement | L2 | > 60% | > 80% |
| **Comms** | Alert Routing Accuracy | L2 | > 90% | > 98% |
| **Comms** | Briefing Actionability Score | L2 | > 3/5 | > 4/5 |

#### L3 — Deep / Root Cause (Engineering & Optimization)

| Metric | Level | Phase | Definition | Target |
|--------|:-----:|-------|-----------|--------|
| Output Completeness Rate | L3 | MVP | If 50 SKUs sent to LLM, do all 50 get analysis? | > 95% |
| Prompt Iteration Count per Agent | L3 | MVP | How many prompt revisions before quality target met | Fewer is better |
| Prompt Stability (Variance) | L3 | MVP | Same input → consistent output quality across runs? | Low variance |
| Context Window Utilization % | L3 | MVP → Beta | How much of Claude's context window is consumed | < 80% |
| LLM Latency P50 / P95 | L3 | MVP → Beta | Response time distribution | P50 < 10s, P95 < 30s |
| Retry Rate | L3 | Beta | % of LLM calls that need retry due to error/timeout | < 5% |
| Google Sheets API Latency | L3 | Beta | Read/write response time | < 500ms |
| Sheets Row Count per Tab | L3 | Beta | Data volume growth — approaching scale limits? | < 5,000 active rows |
| False Negative Rate (Missed Events) | L3 | Beta | Real events that occurred but agent failed to detect | < 15% |
| Confidence Calibration | L3 | Beta | When agent says "High Confidence," is it actually more accurate? | Correlation > 0.5 |
| User Override Patterns | L3 | Beta | What do users consistently change in agent outputs? | Identify and learn |
| Forecast Bias Direction | L3 | Beta | Is the model systematically over or under forecasting? | Drift toward ±5% |
| Data Validation Pass Rate (user data) | L3 | Beta | % of incoming user data passing quality checks | > 80% |

---

### Supply Chain & Operations — During Build

#### Baseline Capture (Must Do BEFORE Agent Goes Live for Each User)

##### L1 Baselines to Capture

| Metric | Level | How to Capture | Why Critical |
|--------|:-----:|---------------|-------------|
| Stockout frequency (per month) | L1 | User self-report + historical data review | To prove stockout REDUCTION |
| Fill rate (current %) | L1 | Order management data or user estimate | To prove fill rate IMPROVEMENT |
| Hours/week on manual SC tasks | L1 | User time diary for 1 week | To prove time SAVED |

##### L2 Baselines to Capture

| Metric | Level | How to Capture | Why Critical |
|--------|:-----:|---------------|-------------|
| PO cycle time (trigger → supplier) | L2 | Measure 5 recent POs | To prove procurement SPEED |
| Supplier on-time rate (estimated) | L2 | User estimate + spot-check 10 POs | To benchmark supplier IMPROVEMENT |
| Inventory turnover (current) | L2 | Financial data | To prove inventory EFFICIENCY |
| Report preparation time | L2 | User self-report | To prove automation VALUE |

##### L3 Baselines to Capture

| Metric | Level | How to Capture | Why Critical |
|--------|:-----:|---------------|-------------|
| Disruption count (last 6 months) | L3 | User recall during onboarding interview | To prove risk DETECTION |
| Average disruption detection time | L3 | User recall | To prove EARLY WARNING |
| Data freshness (how stale is current data) | L3 | Audit their Excel files during onboarding | To prove data CURRENCY |

#### During Beta: Track Agent Impact on SC Metrics

| Metric | Level | Baseline | Week 2 | Week 4 | Week 8 | Target |
|--------|:-----:|----------|--------|--------|--------|--------|
| Stockouts prevented | L1 | 0 (no detection) | | | | > 50% of potential stockouts caught |
| PO cycle time | L2 | [X days] | | | | 50% reduction |
| Report prep time | L2 | [X hours] | | | | 80% reduction |
| Carrier tracking time | L2 | [X hours] | | | | 70% reduction |
| Risks detected proactively | L3 | 0 | | | | ≥ 2 per month |
| Supplier issues flagged before impact | L3 | 0 | | | | ≥ 1 per month |

---

## Stage 3: Production — New Metrics Unlocked by the Agent

### Business & Financial — Production

#### L1 — Surface (Executive Dashboard)

| Metric | Level | Definition | Computed By | Persona |
|--------|:-----:|-----------|------------|---------|
| ⭐ Agent ROI (₹ Return Multiple) | L1 | (Total ₹ saved by agent) / (₹ spent on agent) | Comms Agent (monthly report) | VP Ops, CEO |
| ⭐ Prevented Stockout Value | L1 | ₹ revenue saved by preventing stockouts that would have occurred without agent | Inventory Agent × Demand Agent | VP Ops, SCM |
| Total Cost Savings (monthly) | L1 | Sum of all optimization savings: inventory + procurement + logistics | All agents | VP Ops |
| Working Capital Freed | L1 | ₹ reduction in inventory value while maintaining/improving fill rate | Inventory Agent | VP Ops, CFO |
| Revenue Protected by Risk Mitigation | L1 | ₹ revenue that was at risk from disruptions the agent mitigated | Risk Agent | VP Ops |

#### L2 — Diagnostic

| Metric | Level | Definition | Computed By | Persona |
|--------|:-----:|-----------|------------|---------|
| Inventory Carrying Cost Reduction | L2 | ₹ saved from lower overstock + faster dead stock clearance | Inventory Agent | SCM, VP Ops |
| Emergency Procurement Spend (trending down) | L2 | ₹ spent on rush orders — should decline as agent prevents them | Procurement Agent | Procurement, VP Ops |
| Maverick Spend Reduction | L2 | % of purchases moved back to preferred suppliers | Procurement Agent | Procurement |
| Supplier Renegotiation Savings | L2 | ₹ saved from data-backed contract renegotiations | Supplier Agent | Procurement |
| Logistics Cost Optimization | L2 | ₹ saved from better carrier selection, consolidation | Logistics Agent | Logistics, VP Ops |
| Time Reallocation Value | L2 | Hours saved × team hourly cost = ₹ value of reclaimed time | Comms Agent | VP Ops |

#### L3 — Deep / Root Cause

| Metric | Level | Definition | Computed By | Persona |
|--------|:-----:|-----------|------------|---------|
| Cost per Prevented Stockout Event | L3 | ₹ saved per individual stockout the agent prevented | Inventory + Demand Agents | SCM |
| TCO Improvement per Supplier | L3 | Change in total cost of ownership after data-driven supplier optimization | Supplier Agent | Procurement |
| Freight Cost per Unit per Route (trending) | L3 | Is per-unit shipping cost decreasing over time? | Logistics Agent | Logistics |
| Dead Stock Clearance Rate | L3 | % of flagged dead stock items that were actioned within 30 days | Inventory Agent | SCM |
| Volume Consolidation Savings | L3 | ₹ saved by aggregating purchases across departments/locations | Procurement Agent | Procurement |
| Working Capital Efficiency Ratio | L3 | Revenue per ₹ of inventory — is it improving? | Demand + Inventory Agents | VP Ops, CFO |

#### The ROI Calculation (L1 — The Most Important Number)

```
┌─────────────────────────────────────────────────────────────┐
│  AGENT ROI — MONTHLY CALCULATION                            │
│                                                             │
│  SAVINGS (₹):                                              │
│  ├── Prevented stockout value        [L1] ₹ ________      │
│  ├── Inventory carrying cost saved   [L2] ₹ ________      │
│  ├── Emergency procurement avoided   [L2] ₹ ________      │
│  ├── Logistics optimization          [L2] ₹ ________      │
│  ├── Time saved (hrs × rate)         [L2] ₹ ________      │
│  └── Risk mitigation value           [L1] ₹ ________      │
│                                     ──────────────────      │
│  TOTAL SAVINGS                           ₹ ________       │
│                                                             │
│  COST (₹):                                                 │
│  ├── Subscription                        ₹ ________       │
│  └── API / infrastructure                ₹ ________       │
│                                     ──────────────────      │
│  TOTAL COST                              ₹ ________       │
│                                                             │
│  ═══════════════════════════════════════════════════════    │
│  ROI MULTIPLE = Savings / Cost         = ____×             │
│  Target: > 5× (if we cost ₹25K/mo, we should save ₹125K+) │
│  ═══════════════════════════════════════════════════════    │
└─────────────────────────────────────────────────────────────┘
```

---

### Technical — Production

#### L1 — Surface (Ops Dashboard)

| Metric | Level | Definition | SLA | Alert If |
|--------|:-----:|-----------|:---:|----------|
| Pipeline Uptime | L1 | % of days where full 7-workflow pipeline completes | > 99% | Misses 2+ days |
| Workflow Success Rate (aggregate) | L1 | % of all workflow executions completing without error | > 98% | < 95% |
| Monthly Infrastructure Cost | L1 | Total ₹ spent on n8n + Claude API + Google | < ₹2,000/user | > ₹2,500/user |

#### L2 — Diagnostic (Agent Health)

| Metric | Level | Definition | Target | Alert If |
|--------|:-----:|-----------|:------:|----------|
| Per-Workflow Success Rate | L2 | Success rate broken down by each of 7 workflows | > 98% each | Any workflow < 95% |
| Average Execution Time per Workflow | L2 | Minutes per workflow — trending over time | < 5 min | > 8 min |
| LLM JSON Parse Success Rate | L2 | % of responses that are valid structured output | > 98% | < 95% |
| Forecast Accuracy Trend (4-week rolling) | L2 | Is MAPE stable, improving, or degrading? | Stable or improving | Degrades 3 consecutive weeks |
| PO Approval Rate Trend | L2 | Are users approving more or fewer agent POs? | Stable or improving | Drops below 60% for 2 weeks |
| Alert Dismissal Rate Trend | L2 | Are users ignoring more alerts over time? | Stable or declining | Rises above 30% for 2 weeks |
| Briefing Open Rate Trend | L2 | Are users still reading daily briefings? | > 70% | Drops below 50% for 2 weeks |
| Data Quality Score per User | L2 | Composite: completeness + freshness + consistency | > 70/100 | < 50/100 |

#### L3 — Deep / Root Cause (Engineering)

| Metric | Level | Definition | Target | Action |
|--------|:-----:|-----------|:------:|--------|
| Token Waste Ratio | L3 | Tokens on failed/retried calls vs. total | < 5% | Optimize prompts |
| Prompt Version Performance (A/B) | L3 | Quality comparison across prompt versions | Track | Deploy better version |
| LLM Latency P50 / P95 (production) | L3 | Response time distribution under real load | P50 < 10s, P95 < 25s | Scale or optimize |
| Google Sheets Row Count Growth Rate | L3 | How fast is data volume growing per tab? | Monitor | Archive old data before limits |
| API Rate Limit Proximity | L3 | How close to Anthropic/Google rate limits are we? | < 60% of limit | Implement throttling |
| Error Type Distribution | L3 | Breakdown: timeout vs. parse error vs. API error vs. data error | Track | Fix dominant error type |
| Model Drift Detection Signal | L3 | Statistical test: has output quality distribution shifted? | Stable | Investigate + retune prompts |
| User Override Pattern Analysis | L3 | What do users consistently change? (supplier, qty, urgency) | Track | Learn and adapt agent behavior |
| Confidence Calibration Accuracy | L3 | When agent says High/Med/Low confidence, does accuracy match? | Strong correlation | Adjust calibration thresholds |
| Cross-Module Data Consistency | L3 | Do all 7 agents reference the same current data? | 100% consistent | Fix sync issues |

---

### Supply Chain & Operations — Production

#### L1 — Surface (What the VP Sees Every Morning)

| Metric | Level | Definition | Before | After | Agent |
|--------|:-----:|-----------|--------|-------|-------|
| ⭐ Supply Chain Health Score | L1 | Composite 0-100 score across all dimensions | DID NOT EXIST | Updated daily | Comms Agent |
| Fill Rate / Service Level | L1 | % of orders fulfilled completely from stock | ~90% (guess) | 95%+ (measured per SKU, per channel, weekly) | Inventory Agent |
| Stockout Count (monthly) | L1 | Number of SKU-location stockout events | Unknown (reactive) | Tracked, trending toward zero | Inventory Agent |
| On-Time Delivery Rate | L1 | % of customer shipments arriving on time | ~85% (rough) | Tracked per carrier, per route, trended | Logistics Agent |
| Inventory Turnover Ratio | L1 | How efficiently inventory converts to sales | 4-8× (aggregate) | Per SKU, per category, trended | Inventory Agent |
| Active Risk Count by Severity | L1 | Current supply chain risks being monitored | 0 (no visibility) | Real-time risk register | Risk Agent |

#### L2 — Diagnostic (What the Managers Dig Into)

##### Demand & Forecasting

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Forecast Accuracy (MAPE per SKU) | L2 | Not measured → < 20%, tracked weekly per SKU | Demand |
| Forecast Bias | L2 | Unknown (chronic over-ordering) → ±5%, auto-corrected | Demand |
| Demand Anomaly Detection Rate | L2 | 0% (all surprises) → > 75% of anomalies caught early | Demand |
| Stockout Prediction Horizon | L2 | 0 days (reactive) → 3-14 days advance warning | Inventory + Demand |
| Demand Classification per SKU | L2 | Not done → Every SKU: Stable/Variable/Lumpy/New | Demand |

##### Inventory

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Days of Inventory per SKU per Location | L2 | Not tracked → Calculated daily, auto-updated | Inventory |
| Inventory Health Distribution | L2 | Unknown → Real-time: X% Crit, Y% Low, Z% Healthy, W% Over | Inventory |
| Dead Stock Value (₹) | L2 | Found at annual audit → Flagged within 60 days with actions | Inventory |
| Overstock Value (₹) | L2 | Unknown → Flagged weekly with recommended actions | Inventory |
| Inter-Warehouse Imbalance Alerts | L2 | Not detected → Auto-detected with transfer suggestions | Inventory |
| PO Cycle Time | L2 | 1-3 days → < 4 hours (< 1 hr in mature production) | Procurement |
| PO Automation Rate | L2 | 0% (all manual) → > 60% agent-generated | Procurement |

##### Supplier

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Supplier Composite Score (0-100) | L2 | Didn't exist → Updated weekly for every supplier | Supplier |
| Supplier On-Time Delivery Rate | L2 | Anecdotal → Calculated from every PO, trended | Supplier |
| Supplier Trend Direction (↑→↓) | L2 | Unknown → Per supplier: improving, stable, declining | Supplier |
| Contract Expiry Countdown | L2 | Missed repeatedly → Auto-alert at 90, 60, 30 days | Supplier |
| Single-Source Dependency Map | L2 | Unknown → Auto-identified and flagged | Supplier |

##### Logistics

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Unified Shipment Status | L2 | 3-5 carrier portals → Single dashboard | Logistics |
| Delay Prediction (advance) | L2 | 0 days (reactive) → 1-3 days advance warning | Logistics |
| Shipment Exception Rate | L2 | Unknown → Tracked per carrier, per route | Logistics |
| Carrier Performance Ranking | L2 | Not done → Scored by cost, speed, reliability | Logistics |
| Delay-to-Stockout Impact Map | L2 | Not done → Automatic: delayed shipment → affected SKUs | Logistics |

##### Risk

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Risk Detection Lead Time | L2 | 0 (surprises only) → 1-7 days advance warning | Risk |
| Risk-to-Supply-Chain Map | L2 | Not done → Every risk linked to suppliers, SKUs, routes, ₹ exposure | Risk |
| Disruption Count per Quarter | L2 | Not tracked → Logged with full detail and response | Risk |
| Mitigation Action Effectiveness | L2 | Unknown → Tracked: did the action reduce impact? | Risk |

##### Communication & Process

| Metric | Level | Before → After | Agent |
|--------|:-----:|----------------|-------|
| Decision Audit Completeness | L2 | 0% (decisions in people's heads) → 100% logged with reasoning | Comms |
| Alert-to-Action Time | L2 | Unknown → Measured: hours from alert to user action | Comms |
| Stakeholder Information Freshness | L2 | Days to weeks stale → Updated daily | Comms |
| Report Preparation Time | L2 | 2-5 hrs/week → 0 (fully automated) | Comms |

#### L3 — Deep / Root Cause (What the Agent Analyzes to Drive L2)

##### Demand Deep Metrics

| Metric | Level | Definition | Agent | Why L3 |
|--------|:-----:|-----------|-------|--------|
| Demand Coefficient of Variation per SKU | L3 | How volatile each SKU's demand is — drives safety stock calc | Demand | High CV → more safety stock needed → directly impacts L2 DOI |
| Seasonality Index per SKU | L3 | Quantified seasonal demand patterns per product | Demand | Drives forecast adjustments → improves L2 MAPE |
| Promotional Lift Factor | L3 | How much do promotions increase demand? (historical analysis) | Demand | Enables what-if simulations → better L2 forecasts |
| Cannibalization / Halo Effects | L3 | Does SKU-A's promotion reduce SKU-B's demand? | Demand | Refines forecast → reduces L2 anomaly false positives |
| New Product Demand Analog Matching | L3 | For new SKUs with no history, which existing SKU's pattern to use? | Demand | Enables forecasting new products → prevents L2 blind spots |

##### Inventory Deep Metrics

| Metric | Level | Definition | Agent | Why L3 |
|--------|:-----:|-----------|-------|--------|
| Dynamic Safety Stock per SKU | L3 | Calculated from demand variability × lead time variability × service target | Inventory | Drives L2 reorder points → prevents L1 stockouts |
| Reorder Point Sensitivity Analysis | L3 | How much does fill rate change if ROP shifts by ±10%? | Inventory | Optimizes L2 reorder recommendations |
| Inventory Aging Distribution | L3 | Age breakdown of stock: 0-30, 30-60, 60-90, 90+ days | Inventory | Early warning for L2 dead stock before it's officially "dead" |
| ABC/XYZ Segmentation | L3 | A=high value × X=stable demand → different strategies per segment | Inventory | Drives differentiated L2 policies per SKU category |
| Economic Order Quantity (EOQ) vs. Actual | L3 | Are we ordering optimal quantities or over/under? | Procurement | Tunes L2 quantity recommendations |

##### Supplier Deep Metrics

| Metric | Level | Definition | Agent | Why L3 |
|--------|:-----:|-----------|-------|--------|
| Supplier Defect Rate per Product Type | L3 | Defects broken down by what's being supplied | Supplier | Reveals if L2 quality score is product-specific or systemic |
| Lead Time Distribution (not just average) | L3 | Full histogram of actual lead times — reveals long tail | Supplier | Avg is misleading — the tail drives L2 safety stock needs |
| Supplier Financial Health Signals | L3 | News, payment behavior, industry risk indicators | Risk + Supplier | Early warning for L2 supplier score decline |
| Tier 2/3 Supplier Risk | L3 | Are YOUR supplier's suppliers at risk? | Risk | The hidden risk that causes L2 surprise disruptions |
| Price Trend vs. Market Benchmark | L3 | Is supplier's pricing drifting above market? | Supplier | Triggers L2 renegotiation recommendations |

##### Logistics Deep Metrics

| Metric | Level | Definition | Agent | Why L3 |
|--------|:-----:|-----------|-------|--------|
| Carrier Performance by Route Segment | L3 | Same carrier performs differently on different routes | Logistics | Enables route-specific L2 carrier selection |
| Delivery Time Distribution by Day-of-Week | L3 | Are Monday deliveries slower than Thursday? | Logistics | Optimizes L2 shipment scheduling |
| Weight/Volume Utilization per Shipment | L3 | Are we shipping partial trucks? | Logistics | Identifies L2 consolidation opportunities → L1 cost savings |
| Last-Mile Failure Patterns | L3 | Geographic or time-based patterns in delivery failures | Logistics | Fixes root cause of L2 exception rate |
| Carbon Footprint per Route Option | L3 | CO2 per route for sustainability reporting | Logistics | Emerging L1 requirement for ESG reporting |

##### Risk Deep Metrics

| Metric | Level | Definition | Agent | Why L3 |
|--------|:-----:|-----------|-------|--------|
| Risk Velocity (how fast is risk escalating?) | L3 | Rate of change of risk severity over time | Risk | Distinguishes slow-burn vs. fast-hit risks for L2 prioritization |
| Cascading Impact Simulation | L3 | If Supplier X fails, what's the domino effect on 5 SKUs, 3 warehouses? | Risk | Quantifies the L2 risk-to-supply-chain map in ₹ |
| Historical Disruption Pattern Analysis | L3 | Do disruptions follow seasonal/cyclical patterns? | Risk | Predictive: proactively increase L2 safety stock before high-risk periods |
| Contingency Plan Activation Time | L3 | When playbook triggers, how long until backup is operational? | Risk | Measures L2 recovery time effectiveness |
| Risk Concentration Heat Map | L3 | Geographic/supplier/route concentration of total risk | Risk | Drives strategic L2 diversification decisions |

---

## Master Summary: Metrics by Level Across All Stages

### Count Summary

#### Before (Pain State)

| Lens | L1 Surface | L2 Diagnostic | L3 Root Cause | Total | % Tracked |
|------|:----------:|:-------------:|:-------------:|:-----:|:---------:|
| Business & Financial | 5 | 6 | 5 | 16 | ~15% |
| Technical | 3 | 4 | 3 | 10 | ~10% |
| Supply Chain & Ops | 5 | 7 | 10 | 22 | ~25% |
| **TOTAL** | **13** | **17** | **18** | **48** | **~18%** |

> **82% of these metrics are NOT tracked at all before the agent.**

#### During Build (Agent Metrics)

| Lens | L1 Surface | L2 Diagnostic | L3 Root Cause | Total |
|------|:----------:|:-------------:|:-------------:|:-----:|
| Business & Financial | 4 | 6 | 4 | 14 |
| Technical (AI/Agent) | 4 | 20+ | 14 | 38+ |
| Supply Chain (Baseline) | 3 | 4 | 3 | 10 |
| **TOTAL** | **11** | **30+** | **21** | **62+** |

> **L2 dominates during build — because you're tuning AGENT QUALITY.**

#### After (Production — New)

| Lens | L1 Surface | L2 Diagnostic | L3 Root Cause | Total |
|------|:----------:|:-------------:|:-------------:|:-----:|
| Business & Financial | 5 | 6 | 6 | 17 |
| Technical | 3 | 8 | 10 | 21 |
| Supply Chain & Ops | 6 | 25+ | 15+ | 46+ |
| **TOTAL** | **14** | **39+** | **31+** | **84+** |

> **All levels are rich in production — you now have FULL visibility.**

---

### How Levels Connect: The Diagnostic Cascade

#### Example 1: Stockout Investigation

```
L1 ALERT: Fill Rate dropped to 91% (target: 95%)
    │
    ▼ WHY? Dig into L2...
L2 DIAGNOSIS: SKU-041 and SKU-067 had stockouts this week
    │           Days of Inventory was 0 for both
    │           Reorder was triggered but PO was late
    │
    ▼ WHY? Dig into L3...
L3 ROOT CAUSE:
    ├── SKU-041: Supplier-B lead time variance was 12 days (normally 7)
    │            → Safety stock was calibrated for 7-day lead time
    │            → Not enough buffer for the long tail
    │            → FIX: Increase safety stock OR switch to Supplier-A (faster)
    │
    └── SKU-067: Demand spiked 35% (seasonal — Diwali prep)
                 → Forecast didn't account for seasonal pattern
                 → FIX: Add seasonality index to forecast model
```

#### Example 2: Cost Overrun Investigation

```
L1 ALERT: Agent ROI dropped from 8× to 4× this month
    │
    ▼ WHY? Dig into L2...
L2 DIAGNOSIS: Emergency procurement spend spiked ₹3,00,000
    │           3 rush orders placed at 30% premium
    │           Caused by 2 delayed shipments from Supplier-C
    │
    ▼ WHY? Dig into L3...
L3 ROOT CAUSE:
    ├── Supplier-C had a factory incident (risk agent detected 2 days late)
    │   → Risk detection lead time was only 1 day vs. 3-day target
    │   → News source for Supplier-C's region was not being scanned
    │   → FIX: Add regional news sources for all Tier 1 supplier locations
    │
    └── Backup supplier was not pre-qualified for these SKUs
        → Single-source dependency was flagged but not acted on
        → FIX: Mandate backup supplier qualification for all A-class SKUs
```

#### Example 3: Agent Quality Investigation

```
L1 ALERT: Workflow Success Rate dropped to 93% (target: 98%)
    │
    ▼ WHY? Dig into L2...
L2 DIAGNOSIS: Demand Forecasting workflow failing 3× per week
    │           JSON Parse Success Rate for Demand Agent: 82% (target: 95%)
    │
    ▼ WHY? Dig into L3...
L3 ROOT CAUSE:
    ├── User added 30 new SKUs with no sales history
    │   → LLM returns "I cannot forecast" in plain text instead of JSON
    │   → Data validation didn't catch SKUs with < 8 weeks history
    │   → FIX: Add pre-filter in Function node — exclude new SKUs from
    │          batch, handle separately with analog matching
    │
    └── Prompt was not explicit about handling edge cases
        → FIX: Add instruction: "For SKUs with < 8 weeks of data,
               return confidence: 'Insufficient Data' in JSON format"
```

---

### Persona → Level Mapping

#### VP Operations (Sunita) — PRIMARILY L1

| What She Sees Daily | Level | Source |
|--------------------|:-----:|--------|
| Supply Chain Health Score (0-100) | L1 | Comms Agent briefing |
| Fill Rate (%) | L1 | Inventory Agent |
| Agent ROI (₹ multiple) | L1 | Monthly report |
| Active Risk Count | L1 | Risk Agent |
| Total Cost Savings this month | L1 | Comms Agent |
| Top 3 risks with one-line descriptions | L1→L2 | Risk Agent |
| Inventory Turnover trend | L1→L2 | Inventory Agent |

> **Sunita drills into L2 only when L1 signals a problem. She never sees L3 — that's for her team and the agent.**

#### Supply Chain Manager (Rajesh) — PRIMARILY L2

| What He Sees Daily | Level | Source |
|-------------------|:-----:|--------|
| Health Score + trend | L1 | Comms Agent |
| Inventory Health Distribution (Crit/Low/OK/Over) | L2 | Inventory Agent |
| Days of Inventory for flagged SKUs | L2 | Inventory Agent |
| Forecast accuracy (weekly MAPE) | L2 | Demand Agent |
| Demand anomalies flagged | L2 | Demand Agent |
| Risk register with severity and mappings | L2 | Risk Agent |
| PO cycle time and automation rate | L2 | Procurement Agent |
| Supplier score trends | L2 | Supplier Agent |
| Stockout predictions (what's at risk) | L2 | Inventory + Demand |
| Inter-warehouse imbalances | L2 | Inventory Agent |

> **Rajesh digs into L3 for root cause analysis during weekly reviews. He uses L1 to communicate upward to Sunita.**

#### Procurement Lead (Priya) — L2 + SOME L3

| What She Sees Daily | Level | Source |
|-------------------|:-----:|--------|
| POs pending approval (with recommendations) | L2 | Procurement Agent |
| Supplier scorecards | L2 | Supplier Agent |
| Supplier on-time delivery rates | L2 | Supplier Agent |
| Contract expiry alerts | L2 | Supplier Agent |
| Maverick spend tracking | L2 | Procurement Agent |
| Emergency procurement spend trend | L2 | Procurement Agent |
| Supplier lead time distributions | L3 | Supplier Agent |
| TCO per supplier | L3 | Supplier Agent |
| Price trend vs. market benchmark | L3 | Supplier Agent |

> **Priya uses L3 for supplier negotiations and sourcing decisions.**

#### Logistics Coordinator (Amit) — L2 + SOME L3

| What He Sees Daily | Level | Source |
|-------------------|:-----:|--------|
| Shipment status dashboard (On Track/At Risk/Overdue) | L2 | Logistics Agent |
| Delay predictions with impact assessment | L2 | Logistics Agent |
| Carrier performance ranking | L2 | Logistics Agent |
| Exception rate per carrier | L2 | Logistics Agent |
| Delay-to-stockout impact mapping | L2 | Logistics + Inventory |
| Carrier performance by route segment | L3 | Logistics Agent |
| Delivery time distribution patterns | L3 | Logistics Agent |
| Freight cost per unit per route | L3 | Logistics Agent |

> **Amit uses L3 for carrier optimization and route decisions.**

#### The Agent Itself — PRIMARILY L3

The AI agent operates at L3 internally to compute L2 outputs:

| What the Agent Processes | Level | Purpose |
|-------------------------|:-----:|---------|
| Demand CV per SKU | L3 | Calculate dynamic safety stock |
| Lead time distribution per supplier | L3 | Calibrate reorder points |
| Seasonality indices | L3 | Adjust demand forecasts |
| ABC/XYZ segmentation | L3 | Differentiate inventory policies |
| Risk velocity and cascade modeling | L3 | Prioritize risk alerts |
| Confidence calibration data | L3 | Self-assess output quality |
| User override patterns | L3 | Learn and adapt behavior |
| Token efficiency data | L3 | Optimize own cost |

> **The agent is the only "persona" that lives at L3 full-time. It translates L3 complexity into L2 insights for managers and L1 summaries for executives.**
