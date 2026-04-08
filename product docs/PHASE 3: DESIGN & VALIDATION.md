# 📦 SupplyChain Agent — AI-Powered Supply Chain Co-Pilot

**Directory:** `/design-and-validation/`  
**Status:** Design Finalized / Validation Planning  
**Version:** 1.0 (MVP)

This document contains the complete UI/UX blueprint for the SupplyChain Agent. Since the MVP operates through existing platforms (Google Sheets, Email, and Slack), these wireframes and flows focus on data structure, notification logic, and user interaction within those ecosystems.

---

## 🎨 Wireframes

### Note on MVP Wireframes
The MVP has no custom UI. Outputs are delivered via **Google Sheets**, **Email**, and **Slack**. Future web dashboard wireframes are included for V2 planning.

#### 1. Google Sheets — Main Dashboard Tab
This serves as the primary "Command Center" for the Supply Chain Manager.

```text
┌─────────────────────────────────────────────────────────────────┐ 
│  📊 SupplyChain Agent — Command Center                          │ 
├─────────────────────────────────────────────────────────────────┤ 
│                                                                 │ 
│  SUPPLY CHAIN HEALTH SCORE: [78/100] 🟡                         │ 
│  Last Updated: 2026-04-07 07:15 AM                              │ 
│                                                                 │ 
│  ┌──────────────┬──────────────┬──────────────┬──────────────┐ │ 
│  │ INVENTORY    │ PROCUREMENT  │ LOGISTICS    │ RISK         │ │ 
│  │ 🔴 3 Critical│ 📋 5 Open PO │ ⚠️ 2 Delayed │ 🟡 1 Medium  │ │ 
│  │ 🟡 8 Low     │ ✅ 12 On Trk │ ✅ 15 On Trk │ 🟢 4 Low     │ │ 
│  │ 🟢 89 Healthy│ 📨 3 Pending │ 📦 8 Delivrd │              │ │ 
│  └──────────────┴──────────────┴──────────────┴──────────────┘ │ 
│                                                                 │ 
│  ACTIONS NEEDED TODAY:                                          │ 
│  1. [CRITICAL] Reorder SKU-041 (Widget X) — 3 days until        │ 
│     stockout — PO draft ready for approval                      │ 
│  2. [WARNING] Supplier-B on-time rate dropped to 72%            │ 
│  3. [INFO] Shipment SHP-0891 arriving today — confirm receipt   │ 
│                                                                 │ 
└─────────────────────────────────────────────────────────────────┘ 
```

#### 2. Email Briefing — Supply Chain Manager (Rajesh)
Daily high-granularity digest sent at 6:00 PM.

```text
┌─────────────────────────────────────────────────────────────────┐ 
│  Subject: 📊 Daily Supply Chain Briefing — April 7, 2026        │ 
├─────────────────────────────────────────────────────────────────┤ 
│                                                                 │ 
│  Good evening Rajesh,                                           │ 
│                                                                 │ 
│  HEALTH SCORE: 78/100 (↓ from 82 yesterday)                     │ 
│                                                                 │ 
│  ⚡ CRITICAL ACTIONS (need your attention today)                │ 
│                                                                 │ 
│  1. STOCKOUT RISK: SKU-041 (Widget X) at Warehouse-North        │ 
│     Current stock: 45 units | Daily demand: 18 units            │ 
│     Days remaining: 2.5 | Lead time: 7 days                     │ 
│     → PO draft ready: 500 units from Supplier-A (₹75,000)       │ 
│     → [APPROVE PO] [MODIFY] [DISMISS]                           │ 
│                                                                 │ 
│  2. SUPPLIER ALERT: Supplier-B delivery rate dropped 72%        │ 
│     Was 89% last month. 3 late deliveries this week.            │ 
│     → Recommend: Schedule performance review                    │ 
│     → Backup supplier available: Supplier-F (score: 81)         │ 
│                                                                 │ 
│  📦 LOGISTICS SUMMARY                                           │ 
│  • 17 active shipments: 15 on track, 2 delayed                  │ 
│  • SHP-0891 arriving today — warehouse notified                 │ 
│  • SHP-0903 delayed by est. 2 days (carrier issue)              │ 
│                                                                 │ 
│  📈 DEMAND UPDATE                                               │ 
│  • 2 SKUs trending up >15%: SKU-012 (+22%), SKU-067 (+17%)      │ 
│  • Forecast accuracy last week: 82% (MAPE: 18%)                 │ 
│                                                                 │ 
│  🛡️ RISK STATUS                                                 │ 
│  • No new critical risks detected                               │ 
│  • Ongoing: Port congestion at Chennai — monitoring             │ 
│                                                                 │ 
│  Have a good evening. Tomorrow's briefing at 6 PM.              │ 
│                                                                 │ 
│  — SupplyChain Agent                                            │ 
└─────────────────────────────────────────────────────────────────┘ 
```

#### 3. Email Briefing — VP Operations (Sunita)
High-level executive summary focusing on KPIs and macro-risks.

```text
┌─────────────────────────────────────────────────────────────────┐ 
│  Subject: 📊 Executive Supply Chain Summary — April 7           │ 
├─────────────────────────────────────────────────────────────────┤ 
│                                                                 │ 
│  Good evening Sunita,                                           │ 
│                                                                 │ 
│  SUPPLY CHAIN HEALTH: 78/100 🟡                                 │ 
│                                                                 │ 
│  THREE KEY NUMBERS:                                             │ 
│  • Fill Rate: 94.2% (target: 95%) — slightly below target       │ 
│  • Inventory Turns: 8.1x (target: 8.5x) — improving             │ 
│  • Freight Cost/Unit: ₹12.40 (target: ₹12.00) — stable          │ 
│                                                                 │ 
│  TOP RISK:                                                      │ 
│  Supplier-B reliability declining. 3 late deliveries            │ 
│  this week. Backup supplier identified if needed.               │ 
│  No action required from you at this time.                      │ 
│                                                                 │ 
│  BIGGEST OPPORTUNITY:                                           │ 
│  Electronics category demand up 19% MoM. Recommend              │ 
│  pre-ordering additional stock to capture growth.               │ 
│                                                                 │ 
│  — SupplyChain Agent                                            │ 
└─────────────────────────────────────────────────────────────────┘ 
```

#### 4. Slack Alert — Critical
Instant notification for high-priority stockout or risk events.

```text
┌─────────────────────────────────────────────────────────────────┐ 
│  #supply-chain-alerts                                           │ 
├─────────────────────────────────────────────────────────────────┤ 
│                                                                 │ 
│  🚨 SupplyChain Agent  9:02 AM                                  │ 
│                                                                 │ 
│  CRITICAL: Stockout Risk Detected                               │ 
│                                                                 │ 
│  SKU-041 (Widget X) — Warehouse North                           │ 
│  • Current stock: 45 units                                      │ 
│  • Daily demand: 18 units                                       │ 
│  • Stock runs out in: ~2.5 days                                 │ 
│  • Supplier lead time: 7 days ⚠️ (won't arrive in time)         │ 
│                                                                 │ 
│  Recommended Action:                                            │ 
│  • Emergency PO to Supplier-A (express: 3-day delivery)         │ 
│  • Transfer 100 units from Warehouse-South (has 340 excess)     │ 
│                                                                 │ 
│  PO draft ready → Check email for approval link                 │ 
│  cc: @rajesh @priya                                             │ 
│                                                                 │ 
└─────────────────────────────────────────────────────────────────┘ 
```

#### 5. Future Web Dashboard (v2 Planning)
A look ahead at the integrated web platform.

```text
┌─────────────────────────────────────────────────────────────────┐ 
│  ┌──────┐  SupplyChain Agent          🔔 3  👤 Rajesh  ⚙️      │ 
│  │ LOGO │  ─────────────────────────────────────────────────── │ 
│  └──────┘                                                       │ 
├────────────┬────────────────────────────────────────────────────┤ 
│            │                                                    │ 
│  📊 Home   │  Supply Chain Health                    78/100 🟡  │ 
│  📦 Invtry │  ┌──────────────────────────────────────────────┐ │ 
│  📈 Demand │  │  [Health Trend Chart — Last 30 Days]          │ │ 
│  👥 Supprs │  └──────────────────────────────────────────────┘ │ 
│  🚚 Logstc │                                                    │ 
│  🛡️ Risk   │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌────────┐ │ 
│  📋 Procur │  │ Invntry │ │ Orders  │ │ Shpmnts │ │ Risks  │ │ 
│  💬 Chat   │  │ 3 Crit  │ │ 5 Open  │ │ 2 Late  │ │ 1 Med  │ │ 
│  📄 Log    │  └─────────┘ └─────────┘ └─────────┘ └────────┘ │ 
│            │                                                    │ 
│            │  ┌──────────────────────────────────────────────┐ │ 
│            │  │  💬 Chat with Agent                         │ │ 
│            │  │                                              │ │ 
│            │  │  You: What's our biggest risk this week?     │ │ 
│            │  │                                              │ │ 
│            │  │  Agent: Your biggest risk is Supplier-B's    │ │ 
│            │  │  declining delivery performance. On-time     │ │ 
│            │  │  rate dropped from 89% to 72% this month.    │ │ 
│            │  │  Three SKUs depend solely on them...         │ │ 
│            │  │                                              │ │ 
│            │  │  [Type a question...]            [Send]      │ │ 
│            │  └──────────────────────────────────────────────┘ │ 
│            │                                                    │ 
└────────────┴────────────────────────────────────────────────────┘ 
```

---

## 🗺️ User Flow Diagrams

### Flow 1: New User Onboarding
1. **User Signs Up** ➔ Receives Welcome Email with Setup Guide.
2. **Download Templates** ➔ Fills Excel templates (Inventory, Sales, Suppliers, POs, Shipments).
3. **Connect Data** ➔ Uploads to Google Sheets and shares with n8n service account.
4. **Configuration** ➔ Admin sets up API keys (Anthropic, Google, Slack) and imports 7 workflow JSONs.
5. **Validation** ➔ Test execution of workflows.
   - **Success** ➔ Onboarding Complete.
   - **Error** ➔ Troubleshooting check.

### Flow 2: Daily Operations
1. **7:00 AM** ➔ Automated Workflows (Demand, Inventory, Risk).
2. **Data Update** ➔ Results written to Google Sheets dashboard.
3. **Critical Issues?** ➔ Yes: Immediate Slack/Email Alert.
4. **Action** ➔ SCM Reviews alert ➔ Approve PO / Approve Transfer / Dismiss.
5. **6:00 PM** ➔ Daily Briefing Email arrives.

### Flow 3: Procurement Cycle
1. **Detection** ➔ Inventory Agent detects low stock.
2. **Workflow** ➔ Triggers Procurement Agent ➔ Claude drafts PO (calculates qty, selects supplier).
3. **Stage** ➔ PO written to Google Sheets as "Draft".
4. **Approval** ➔ Approval Email sent ➔ [APPROVE] / [REJECT].
   - **Approved** ➔ Claude drafts supplier email ➔ Email Sent ➔ 48hr Follow-up.
   - **Rejected** ➔ Reason logged in Decision_Log.

### Flow 4: Risk Event Response
1. **Detection** ➔ Risk Agent detects threat (e.g., Typhoon).
2. **Mapping** ➔ Maps threat to specific Suppliers, SKUs, and Revenue.
3. **Mitigation** ➔ Generates recommendations (Expedite POs, Activate backup).
4. **Communication** ➔ Writes to Risk_Register ➔ Sends Alerts to SCM, Procurement, and VP Ops.
5. **Resolution** ➔ Agent monitors and logs outcome in Register.

---

## 🔗 Prototype Links & Assets

| Asset | Type | Description |
| :--- | :--- | :--- |
| **Google Sheets Template** | MVP Interface | [To be added] Interactive Command Center |
| **Sample Email Briefings** | Mockups | [To be added] HTML templates for each persona |
| **Slack Alert Mockups** | Mockups | [To be added] Critical and Digest variants |
| **n8n Workflow Screens** | Documentation | [To be added] Visual canvas of all 7 workflows |
| **Figma Dashboard (v2)** | Future | [Q3 2026] Interactive web dashboard prototype |
| **Landing Page** | Marketing | [To be added] Waitlist collection site |

---

## 🧪 Usability Test Plan

**Objective:** Validate that beta users can set up and operate the agent with minimal support.

### Test Parameters
- **Participants:** 5-8 beta users.
- **Format:** Remote, moderated (Zoom).
- **Duration:** 60 minutes.
- **Participant Criteria:** Supply chain roles, 50-500 employees, comfortable with Excel/Google Sheets.

### Scenarios
1. **Initial Setup:** Fill templates and verify connection (< 20 mins).
2. **Reading Briefing:** Identify top 3 action items (< 3 mins).
3. **PO Approval:** Decide on a draft PO via email link.
4. **Risk Alert:** Navigate to Risk Register and describe response plan.
5. **Exploration:** General feedback on Google Sheets dashboard.

---

## 📊 A/B Experiment Design

### Experiment 1: Briefing Format
- **Hypothesis:** Health scores increase engagement.
- **A:** Text-only summary.
- **B:** Health score (78/100) at top.
- **Metric:** Email open rate / action rate.

### Experiment 2: Alert Urgency Framing
- **Hypothesis:** Action-oriented subjects reduce response time.
- **A:** "Low stock alert: SKU-041".
- **B:** "Approve PO to prevent SKU-041 stockout in 3 days".
- **Metric:** Time to action.

---

## ♿ Accessibility Checklist

### Email Briefings
- [ ] Semantic HTML (headers, lists).
- [ ] Color contrast > 4.5:1.
- [ ] Text labels alongside color indicators.
- [ ] Alt text for emojis/icons.
- [ ] Readable font (min 14px).

### Google Sheets
- [ ] Descriptive column headers.
- [ ] Patterns + color for conditional formatting.
- [ ] Frozen header rows.
- [ ] Hover explanations for complex fields.

### Slack Alerts
- [ ] Text-based alerts (no info hidden in images).
- [ ] Structured sections (Block Kit).
- [ ] Clear call-to-action language.

---

## 📝 Design Review Notes
*Template for logging feedback (DR-001, DR-002, etc.) and tracking resolution status.*
