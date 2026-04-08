# 📦 SupplyChain Agent — AI-Powered Supply Chain Co-Pilot
-----

## 📂 Directory Structure

`strategy-and-vision/`

  - [Vision Document](https://www.google.com/search?q=%23-vision-document)
  - [Product Principles](https://www.google.com/search?q=%23-product-principles)
  - [OKRs — Q2 2026](https://www.google.com/search?q=%23-okrs--q2-2026-april--june)
  - [Opportunity Assessment](https://www.google.com/search?q=%23-opportunity-assessment)

-----

## 📄 Vision Document

**File:** `vision-doc.md` | **Date:** 2026-04-07

### 1\. Mission

To democratize AI-powered supply chain management for small and mid-sized businesses that cannot afford SAP, Oracle, or Kinaxis — giving them enterprise-grade intelligence at spreadsheet-level simplicity.

### 2\. The Problem We Solve

**Current Reality for SMBs:**

  - **Data lives in silos:** Inventory (Excel), sales (Google Sheets), supplier info (Emails), shipments (Manual).
  - **Reactive Operations:** Teams discover stockouts only when customers complain.
  - **No forecasting:** Planning is "gut-feel" or basic math.
  - **Talent gap:** SMBs cannot afford dedicated data scientists.

**The Cost of Inaction:**

  - **5-15%** revenue lost to stockouts annually.
  - **20-30%** excess inventory carrying costs.
  - **10-25%** of procurement spend is "maverick" (off-contract).

### 3\. Our Solution

An AI agent system that **Ingests** (Excel/PDF), **Reasons** (Claude LLM), **Acts** (Forecasting/Reorders), **Learns** (Outcome optimization), and **Reports** (Persona-based briefings).

### 4\. Target Market & Differentiators

  - **Primary:** SMB Manufacturers/Distributors (50-500 employees, $5M-$100M revenue).
  - **Secondary:** Mid-market teams needing quick-win pilots without 12-month ERP implementations.

| Feature | **SupplyChain Agent** | Traditional SCM | Other AI Tools |
| :--- | :--- | :--- | :--- |
| **Infrastructure** | Zero | Months of setup | Requires APIs/DBs |
| **Data Input** | Excel/PDF | Structured Data Only | API Integrations |
| **Logic** | AI Reasoning | Rule-based | Bolt-on features |
| **Cost** | \< $85/month | $50K-$500K/year | $500-$5,000/mo |

### 5\. 3-Year Roadmap

  - **Year 1 (2026):** MVP with 7 agent modules. 50 paying customers.
  - **Year 2 (2027):** Web dashboard, direct ERP integrations, multi-tenant architecture.
  - **Year 3 (2028):** Autonomous OS — agents negotiate with supplier agents.

-----

## 💡 Product Principles

**File:** `product-principles.md`

1.  **Spreadsheet-Simple, Enterprise-Smart:** If a manager needs training to understand the output, we've failed.
2.  **Proactive Over Reactive:** Don't show me a problem I know; show me the one I don't see coming.
3.  **Human-in-the-Loop, Not Human-in-the-Way:** Automate the obvious, escalate the ambiguous.
4.  **Data Forgiveness:** Real-world data is messy. Use fuzzy matching and graceful degradation.
5.  **Persona-First Design:** VPs get summaries; coordinators get SKU-level tasks.
6.  **Transparent Reasoning:** If the agent can’t explain *why*, it shouldn’t act.
7.  **Start Small, Scale Gracefully:** The MVP architecture must support the transition to a full platform.

-----

## 🎯 OKRs — Q2 2026 (April – June)

**File:** `okrs.md`

### OKR 1: Product Development

| Key Result | Target | Status |
| :--- | :--- | :--- |
| All 7 n8n workflows built and tested | 7/7 | 🔴 Not Started |
| Excel templates finalized with sample data | 5/5 | 🔴 Not Started |
| System prompts validated for accuracy | 7/7 | 🔴 Not Started |
| Average workflow execution time \< 3 minutes | \< 3m | 🔴 Not Started |

### OKR 2: User Validation

| Key Result | Target | Status |
| :--- | :--- | :--- |
| Recruit 10 beta users (SMB teams) | 10 | 🔴 Not Started |
| Achieve NPS \> 30 from beta users | \> 30 | 🔴 Not Started |
| Weekly active users after 4 weeks | 5 | 🔴 Not Started |

-----

## 📈 Opportunity Assessment

**File:** `opportunity-assessment.md`

### 1\. Market Size

  - **TAM:** $28.9B (Global SCM software market).
  - **SAM:** $4.2B (SMB SCM software).
  - **SOM:** $200M-$400M (AI-powered, low-code tools for Excel-native SMBs).

### 2\. Competitive Insight

We operate in a **Blue Ocean**. While SAP and Kinaxis focus on the enterprise "Top 1%," and Tableau provides visuals without action, SupplyChain Agent provides **reasoning and action** for the underserved SMB market.

### 3\. Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
| :--- | :--- | :--- | :--- |
| LLM Hallucinations | Medium | High | Confidence scores & human review |
| Poor Data Quality | High | Medium | Data quality scoring & cleaning suggestions |
| n8n Scaling | Medium | Medium | Migration path to custom backend |
| Data Privacy | Medium | High | On-prem n8n option & clear policies |

### 4\. Go/No-Go Recommendation

**Decision: ✅ GO**
The market gap is clear, technical feasibility via n8n + Claude is proven, and the MVP cost is ultra-low ($85/month).

**Kill Criteria:**

  - \< 3 beta users active after 4 weeks.
  - Forecast accuracy (MAPE) \> 40%.
  - Cost per user exceeds $50/month.

----
