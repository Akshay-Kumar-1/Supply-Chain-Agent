# 📦SupplyChain Agent — AI-Powered Supply Chain Co-Pilot

This directory contains the documentation, specifications, and tracking templates required for the post-launch phase of the **SupplyChain Agent — AI-Powered Supply Chain Co-Pilot**. The primary focus of this phase is to monitor product health, gather user feedback, and iterate toward a robust V2 platform.

## 📂 Directory Structure
`Directory: /post-launch-and-iteration/`

* `analytics-dashboard-spec.md` — Performance and health monitoring.
* `user-feedback-tracker.md` — Centralized log for user input.
* `nps-csat-summary.md` — Sentiment and satisfaction metrics.
* `post-launch-retrospective.md` — Framework for team review.
* `iteration-backlog.md` — Prioritized list of future improvements.
* `bug-feature-triage-matrix.md` — Classification and SLA guide.
* `v2-planning-notes.md` — Vision and architecture for the next major release.

---

## 1. Analytics Dashboard Specification

**Purpose:** Track product health, user engagement, business metrics, and agent performance to inform iteration decisions.

### Implementation Strategy
Analytics will be tracked across the following low-code/no-code stack:
* **Google Sheets:** "Analytics" tab in the master sheet.
* **n8n Execution Logs:** Workflow success/failure data.
* **Anthropic Console:** API usage and costs.
* **Looker Studio (Free):** Connected to Google Sheets for visualization.

### Dashboard 1: Product Health (Operational)
| Metric | Source | Update Frequency |
| :--- | :--- | :--- |
| Workflow execution count (by module) | n8n logs | Daily |
| Workflow success rate (by module) | n8n logs | Daily |
| Average execution time (by module) | n8n logs | Daily |
| Claude API calls per day | Anthropic console | Daily |
| Claude API cost per day | Anthropic console | Daily |
| Google Sheets API operations per day | n8n logs | Daily |
| Error count and types | n8n error logs | Daily |

**Alerting Logic:**
* Workflow success rate < 90% → Slack alert to Dev.
* Daily API cost > $10 → Slack alert to Dev + PM.
* Any SEV-1 error → Immediate Slack alert to all.

**Visualization Mockup:**
```text
┌──────────────────────────────────────────────┐
│  PRODUCT HEALTH DASHBOARD                    │
│                                              │
│  Workflow Success Rate     [====== 96%]      │
│  Avg Execution Time        2.3 min           │
│  API Cost Today            $4.20             │
│  Errors Today              1 (SEV-4)         │
│                                              │
│  [Line chart: execution time trend, 30 days] │
│  [Bar chart: executions by module, 7 days]   │
│  [Area chart: API cost trend, 30 days]       │
└──────────────────────────────────────────────┘
```

### Dashboard 2: User Engagement
| Metric | Definition | Source | Target |
| :--- | :--- | :--- | :--- |
| Total Registered Users | Users with active setup | Signup list | Growth |
| Weekly Active Users (WAU) | Users with ≥1 workflow execution/week | n8n logs | > 60% |
| Daily Active Users (DAU) | Users triggering ≥1 workflow/day | n8n logs | > 30% |
| Briefing Open Rate | % of briefing emails opened | Email tracking | > 70% |
| Alert Action Rate | % of alerts acted upon within 4 hours | Email click tracking | > 50% |
| PO Approval Rate | % of auto-generated POs approved | Google Sheets | > 60% |
| Avg Time to Action | Hours from alert to user action | Timestamp analysis | < 4 hrs |
| Module Usage Dist. | Which modules are used most | n8n logs | Balanced |

**Engagement Funnel:**
Signed Up → Setup Complete → First Briefing Received → First Action Taken → Active Week 1 → Active Week 2 → Active Week 4 → Converted to Paid → Active Month 3.

### Dashboard 3: Business Metrics
| Metric | Source | Frequency |
| :--- | :--- | :--- |
| Total signups | Signup tracking | Daily |
| Conversion: Free → Paid | Stripe | Weekly |
| MRR (Monthly Recurring Revenue) | Stripe | Weekly |
| Churn rate | Stripe | Monthly |
| CAC (Customer Acquisition Cost) | Marketing spend / new customers | Monthly |
| LTV (Lifetime Value) | MRR × avg lifetime | Monthly |
| LTV:CAC Ratio | Calculated | Monthly |
| Cost per active user | (API + infra) / active users | Monthly |
| NPS / CSAT | Survey | Monthly |

### Dashboard 4: Agent Performance
**Per-Module Quality Metrics:**
* **Demand Forecasting:** MAPE (Mean Absolute % Error) via Forecast vs. Actuals.
* **Inventory:** Stockout events post-adoption.
* **Supplier Mgmt:** User agreement with scores (Validation survey).
* **Logistics:** Delay prediction accuracy (Predicted vs. Actual).
* **Risk:** True positive rate on risk alerts.
* **Procurement:** PO approval rate + cycle time.
* **Communication:** Briefing open rate + action rate.

**LLM Quality Tracking:**
* JSON parse success rate.
* Output relevance score (manual review, weekly sample of 20 outputs).
* Hallucination incidents (user-reported inaccuracies).
* Prompt iteration tracking (version performance).

---

## 2. User Feedback Tracker

### Collection Channels
* Weekly feedback calls (beta users).
* Slack/email messages from users.
* Google Form surveys (NPS, CSAT).
* Usability test observations.
* In-app feedback (Future: thumbs up/down on briefings).

### Feedback Log Template
| ID | Date | User | Channel | Module | Type | Feedback | Severity | Status | Action Taken |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FB-001 | | | | | Bug/Feature/UX | | P0-P3 | New/Done | |

### Synthesis (Monthly)
* **Top Themes:** Issues mentioned by multiple users and planned actions.
* **Top Feature Requests:** Demand-driven priority assessment.
* **Sentiment Trend:** Monthly breakdown of Positive/Neutral/Negative sentiment.

---

## 3. NPS & CSAT Summary

### NPS (Net Promoter Score)
**Question:** "How likely are you to recommend SupplyChain Agent to a colleague or friend?" (0-10 scale).
* **Targets:** > 30 for Beta; > 40 for General Availability (GA).

### CSAT (Customer Satisfaction Score)
Measured on a 1-5 scale across all modules and dimensions including:
* Accuracy of recommendations.
* Ease of setup.
* Usefulness of daily briefings.
* Trustworthiness of AI outputs.
* Time saved & Overall value for price.

---

## 4. Post-Launch Retrospective

**Status:** TEMPLATE — To be conducted after Beta Week 4.
**Format:** Start / Stop / Continue + Metrics Review.

| Metric | Target | Actual |
| :--- | :--- | :--- |
| Workflows built | 7 | |
| Beta users onboarded | 10 | |
| Weekly active users | > 5 | |
| NPS | > 30 | |
| Critical bugs | 0 | |
| Avg workflow success rate | > 95% | |
| Time to first value | < 4 hrs | |

---

## 5. Iteration Backlog

| ID | Title | Type | Module | Priority | Effort | Value |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| IT-001 | Prophet statistical forecasting + LLM | Enhancement | Demand | P1 | Large | High |
| IT-002 | PDF auto-ingestion via email | Feature | All | P1 | Medium | High |
| IT-003 | Google Forms PO approval | Enhancement | Procure. | P2 | Small | Medium |
| IT-005 | Data quality scoring | Enhancement | All | P1 | Medium | High |
| IT-010 | Webhook trigger for real-time alerts | Enhancement | All | P1 | Medium | High |
| IT-015 | Onboarding wizard / guided setup | UX | All | P1 | Large | High |

---

## 6. Bug vs. Feature Triage Matrix

### Classification Guide
1.  **Bug:** Something broken that previously worked or incorrect/misleading output.
2.  **Feature Request:** User wants something the product doesn't currently do.
3.  **UX Improvement:** Hard to use but technically working.
4.  **Support/Education:** Related to data quality or user's own data.

### Bug Severity & SLA
* **P0 - Critical:** System down / Data corruption. SLA: **< 2 hours**.
* **P1 - High:** Major feature broken, no workaround. SLA: **< 8 hours**.
* **P2 - Medium:** Feature partially broken, workaround exists. SLA: **< 48 hours**.
* **P3 - Low:** Minor issue, cosmetic. SLA: **Next sprint**.

---

## 7. V2 Planning Notes

**Vision:** Evolve from "AI workflows that output to email and sheets" to "AI platform with a web dashboard, direct integrations, and self-serve experience."

### Key Themes
1.  **Self-Serve Web Experience:** React dashboard, Chat interface, and onboarding wizards.
2.  **Real Data Integration:** APIs for Odoo, Shopify, QuickBooks, and Logistics carriers (Delhivery/FedEx).
3.  **Advanced Intelligence:** Hybrid Prophet/ARIMA + LLM forecasting and anomaly detection.
4.  **Collaboration:** Multi-user accounts (RBAC) and in-app approvals.
5.  **Platform Scalability:** Migration from Google Sheets to PostgreSQL/FastAPI.

### Planned Architecture
```text
┌──────────────────────────────────────────────┐
│           React Web Dashboard                │
│   Chat + Dashboards + Approvals + Settings   │
└───────────────────┬──────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────┐
│           FastAPI Backend                    │
│   Auth + API + Orchestration + WebSockets    │
└───────────┬──────────────────┬───────────────┘
            │                  │
    ┌───────▼──────┐   ┌──────▼───────┐
    │ Agent Engine │   │ Integration  │
    │ (n8n / custom│   │ Layer        │
    │  orchestr.)  │   │ (ERP, WMS,   │
    │              │   │  TMS, APIs)  │
    └───────┬──────┘   └──────┬───────┘
            │                  │
            ▼                  ▼
    ┌──────────────────────────────────┐
    │           Data Layer             │
    │   PostgreSQL + Redis + Vector DB │
    └──────────────────────────────────┘
```

### Timeline & Investment
* **Planning:** 
* **GA Release:** 
* **Estimated Build Cost:** 
