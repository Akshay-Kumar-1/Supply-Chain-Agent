🔗 SupplyChain Agent 

An AI-powered supply chain co-pilot built with n8n + Claude — zero infrastructure required.  

Features • Architecture • Getting Started • Workflows • Data Model • Personas • Roadmap • Contributing • License  

 

 

🧠 What Is This? 

SupplyChain Agent is an MVP supply chain management system powered by AI. It uses n8n workflows as the orchestration engine and Claude (Anthropic) as the reasoning layer to monitor inventory, forecast demand, manage suppliers, track logistics, detect risks, automate procurement, and coordinate communication — all from Excel/CSV files and PDFs as input. 

No databases. No custom APIs. No cloud infrastructure. Just spreadsheets, an LLM, and smart automation. 

Excel/PDF  ──→  n8n Workflows  ──→  Claude LLM  ──→  Alerts, Reports, Actions 
  

 

✨ Features 

7 Autonomous Agent Modules 

# 
Agent 
What It Does 
1 
Demand Forecasting 
Predicts future demand per SKU using sales history, flags anomalies, supports what-if scenarios 
2 
Inventory Optimization 
Monitors stock health, calculates dynamic reorder points, triggers replenishment, detects dead stock 
3 
Supplier Management 
Scores suppliers on delivery/quality/cost, identifies risks, flags contract expirations 
4 
Logistics Monitoring 
Tracks shipments, predicts delays, recommends rerouting and escalation actions 
5 
Risk & Disruption 
Scans external threats (weather, geopolitical, port congestion) and maps to your supply chain 
6 
Procurement 
Auto-generates POs from inventory triggers, recommends suppliers, manages approval workflows 
7 
Communication 
Sends persona-specific daily briefings, routes alerts, maintains decision audit trails 
Key Highlights 

🚫 Zero Infrastructure — No databases, servers, or deployments 
📊 Excel/PDF Input — Works with files your team already uses 
🧠 LLM-Powered Reasoning — Claude analyzes, recommends, and drafts actions 
📋 Google Sheets as DB — Persistent, shareable, real-time storage layer 
👤 Persona-Based Outputs — Each role gets tailored briefings and alerts 
⚡ n8n Orchestration — Visual workflow builder, easy to modify and extend 
💰 < $85/month — Total operating cost for the full MVP 
 

🏗️ Architecture 

┌─────────────────────────────────────────────────────────────┐ 
│                     TRIGGER LAYER                           │ 
│            Schedule / Email / Webhook / Manual               │ 
└─────────────┬───────────────────────────────┬───────────────┘ 
              │                               │ 
              ▼                               ▼ 
┌──────────────────────┐       ┌──────────────────────────┐ 
│  DATA INGESTION      │       │  PDF PARSER              │ 
│  Excel / CSV /       │       │  Extract text via        │ 
│  Google Sheets       │       │  n8n PDF node + LLM      │ 
└──────────┬───────────┘       └────────────┬─────────────┘ 
           │                                │ 
           ▼                                ▼ 
┌─────────────────────────────────────────────────────────────┐ 
│                   LLM REASONING LAYER                       │ 
│          Claude (Anthropic) via n8n AI Nodes                │ 
│   Structured prompts → JSON analysis → Decisions            │ 
└─────────────────────────┬───────────────────────────────────┘ 
                          │ 
                          ▼ 
┌─────────────────────────────────────────────────────────────┐ 
│                     OUTPUT LAYER                            │ 
│   Google Sheets │ Email │ Slack │ Excel Reports             │ 
└─────────────────────────────────────────────────────────────┘ 
  

Inter-Agent Data Flow 

Demand Forecast ──→ Inventory Agent ──→ Procurement Agent ──→ Supplier Agent 
      │                    │                    │                    │ 
      │                    ▼                    ▼                    │ 
      │              Logistics Agent ◄──────────┘                   │ 
      │                    │                                        │ 
      ▼                    ▼                                        ▼ 
Risk Agent ◄───────────────────────────────────────────────────────┘ 
      │ 
      ▼ 
Communication Agent ──→ Personalized Briefings per Persona 
  

 

🚀 Getting Started 

Prerequisites 

Tool 
Purpose 
Link 
n8n 
Workflow orchestration 
n8n.io (cloud or self-hosted) 
Anthropic API Key 
Claude LLM access 
console.anthropic.com 
Google Account 
Sheets as DB + Drive for file storage 
sheets.google.com 
Slack Workspace (optional) 
Real-time alerts 
slack.com 
Step 1 — Clone the Repository 

git clone https://github.com/yourusername/supplychain-agent.git 
cd supplychain-agent 
  

Step 2 — Set Up Google Sheets 

Open templates/google_sheets_template.xlsx from this repo 
Upload it to Google Sheets — this creates your "database" 
The template contains these tabs: 
Tab Name 
Purpose 
Inventory_Master 
Current stock levels per SKU per warehouse 
Sales_History 
Historical sales data for demand forecasting 
Supplier_Master 
Supplier directory with performance baselines 
Purchase_Orders 
All POs (draft, approved, in-transit, received) 
Shipments_Tracking 
Shipment status and delivery tracking 
Demand_Forecasts 
Output: LLM-generated demand predictions 
Inventory_Actions 
Output: Reorder recommendations and alerts 
Supplier_Scores 
Output: Supplier scorecards and rankings 
Logistics_Dashboard 
Output: Shipment status and exception flags 
Risk_Register 
Output: Active risks with severity and mitigation 
Comms_Log 
Output: Audit trail of all agent communications 
Decision_Log 
Output: Record of all automated decisions 
Share the Google Sheet with your n8n service account email 
Step 3 — Import n8n Workflows 

Open your n8n instance 
Go to Workflows → Import 
Import each workflow JSON file from the workflows/ folder: 
workflows/ 
├── 01_demand_forecasting_agent.json 
├── 02_inventory_optimization_agent.json 
├── 03_supplier_management_agent.json 
├── 04_logistics_monitoring_agent.json 
├── 05_risk_disruption_agent.json 
├── 06_procurement_agent.json 
└── 07_communication_agent.json 
  

Step 4 — Configure Credentials in n8n 

Anthropic (Claude): Add your API key under Settings → Credentials → Anthropic 
Google Sheets: Connect via OAuth2 under Settings → Credentials → Google Sheets 
Gmail / Outlook: Connect your email account for sending alerts 
Slack (optional): Connect via OAuth2 for real-time notifications 
Step 5 — Populate Your Data 

Fill in the Excel templates with your actual data: 

templates/ 
├── inventory_master.xlsx 
├── sales_history.xlsx 
├── supplier_master.xlsx 
├── purchase_orders.xlsx 
└── shipments_tracking.xlsx 
  

Upload them to the Google Sheet or use the import feature. 

Step 6 — Activate Workflows 

Enable each workflow in n8n. They will run on their configured schedules: 

Time 
Workflow 
6:00 AM 
Risk & Disruption Agent 
7:00 AM 
Demand Forecast (weekly) + Inventory Check (daily) 
7:30 AM 
Procurement Agent (triggered by inventory) 
9:00 AM 
Logistics Check #1 
3:00 PM 
Logistics Check #2 
5:00 PM 
Supplier Scoring (weekly, Fridays) 
6:00 PM 
Communication Agent — End-of-Day Briefings 
 

📂 Repository Structure 

supplychain-agent/ 
│ 
├── README.md 
├── LICENSE 
├── CONTRIBUTING.md 
├── CHANGELOG.md 
│ 
├── assets/ 
│   ├── logo.png 
│   ├── architecture_diagram.png 
│   └── screenshots/ 
│       ├── inventory_dashboard.png 
│       ├── risk_briefing_email.png 
│       └── slack_alerts.png 
│ 
├── templates/ 
│   ├── google_sheets_template.xlsx        # Master Google Sheets template 
│   ├── inventory_master.xlsx              # Sample inventory data 
│   ├── sales_history.xlsx                 # Sample sales history 
│   ├── supplier_master.xlsx               # Sample supplier directory 
│   ├── purchase_orders.xlsx               # Sample PO data 
│   └── shipments_tracking.xlsx            # Sample shipment data 
│ 
├── workflows/ 
│   ├── 01_demand_forecasting_agent.json 
│   ├── 02_inventory_optimization_agent.json 
│   ├── 03_supplier_management_agent.json 
│   ├── 04_logistics_monitoring_agent.json 
│   ├── 05_risk_disruption_agent.json 
│   ├── 06_procurement_agent.json 
│   └── 07_communication_agent.json 
│ 
├── prompts/ 
│   ├── demand_analyst.md                  # System prompt for demand agent 
│   ├── inventory_manager.md               # System prompt for inventory agent 
│   ├── supplier_analyst.md                # System prompt for supplier agent 
│   ├── logistics_coordinator.md           # System prompt for logistics agent 
│   ├── risk_director.md                   # System prompt for risk agent 
│   ├── procurement_manager.md             # System prompt for procurement agent 
│   └── chief_of_staff.md                  # System prompt for communication agent 
│ 
└── docs/ 
    ├── setup_guide.md                     # Detailed setup instructions 
    ├── data_model.md                      # Full data model documentation 
    ├── prompt_engineering.md              # How to customize agent prompts 
    ├── troubleshooting.md                 # Common issues and fixes 
    └── graduation_guide.md               # When & how to scale beyond MVP 
  

 

📊 Data Model 

Input Files 

inventory_master.xlsx 

Column 
Type 
Description 
SKU_ID 
String 
Unique product identifier 
Product_Name 
String 
Human-readable product name 
Category 
String 
Product category 
Warehouse 
String 
Storage location 
Current_Stock 
Integer 
Units currently in stock 
Reorder_Point 
Integer 
Threshold to trigger reorder 
Safety_Stock 
Integer 
Minimum buffer stock 
Unit_Cost 
Float 
Cost per unit (₹) 
Lead_Time_Days 
Integer 
Supplier delivery lead time 
Primary_Supplier 
String 
Default supplier ID 
Last_Updated 
Date 
Last inventory count date 
sales_history.xlsx 

Column 
Type 
Description 
Date 
Date 
Transaction date 
SKU_ID 
String 
Product sold 
Warehouse 
String 
Fulfillment location 
Quantity_Sold 
Integer 
Units sold 
Channel 
String 
Sales channel (Online/Retail/Wholesale) 
Revenue 
Float 
Sale value (₹) 
supplier_master.xlsx 

Column 
Type 
Description 
Supplier_ID 
String 
Unique supplier identifier 
Supplier_Name 
String 
Company name 
Contact_Email 
String 
Primary contact email 
Products_Supplied 
String 
Comma-separated SKU IDs 
Avg_Lead_Time 
Integer 
Average delivery days 
On_Time_Rate 
Float 
Historical on-time delivery % 
Defect_Rate 
Float 
Historical defect % 
Price_Competitiveness 
String 
Low / Medium / High 
Contract_Expiry 
Date 
Contract end date 
Risk_Level 
String 
Low / Medium / High 
purchase_orders.xlsx 

Column 
Type 
Description 
PO_ID 
String 
Purchase order number 
SKU_ID 
String 
Product being ordered 
Supplier_ID 
String 
Supplier fulfilling order 
Quantity 
Integer 
Units ordered 
Order_Date 
Date 
PO creation date 
Expected_Delivery 
Date 
Expected arrival date 
Status 
String 
Draft / Approved / In Transit / Delivered 
Actual_Delivery 
Date 
Actual arrival date (filled on receipt) 
shipments_tracking.xlsx 

Column 
Type 
Description 
Shipment_ID 
String 
Tracking reference 
PO_ID 
String 
Linked purchase order 
Carrier 
String 
Shipping carrier name 
Origin 
String 
Ship-from location 
Destination 
String 
Ship-to location 
Ship_Date 
Date 
Date shipped 
Expected_Arrival 
Date 
ETA 
Current_Status 
String 
In Transit / Delivered / Delayed 
Delay_Flag 
Boolean 
Is shipment delayed? 
 

👤 Personas 

The system generates role-specific outputs for four personas: 

Persona 
Primary Modules 
What They Receive 
Supply Chain Manager 
Demand, Inventory, Risk, Communication 
Daily health dashboard, critical alerts, what-if analysis, risk briefings 
Procurement Lead 
Procurement, Supplier Management, Communication 
PO drafts for approval, supplier scorecards, spend analytics, contract alerts 
Logistics Coordinator 
Logistics, Communication 
Shipment exception alerts, delay predictions, carrier performance data 
C-Suite / VP Operations 
Risk, Communication 
Executive summary (3 KPIs + top risk + biggest opportunity), cost trends 
 

🗺️ Roadmap 

✅ v0.1 — Current MVP 

7 agent workflows in n8n 
Excel/PDF input support 
Google Sheets as persistent storage 
Email + Slack alert routing 
Persona-based daily briefings 
Claude-powered reasoning and analysis 
🔜 v0.2 — Enhanced Intelligence 

Statistical forecasting models (Prophet) alongside LLM analysis 
PDF auto-ingestion via email (forward invoices/reports to a dedicated inbox) 
Approval workflows with Google Forms integration 
Historical trend dashboards via Looker Studio / Google Sheets charts 
Webhook triggers for real-time event processing 
🔮 v0.3 — Platform Graduation 

PostgreSQL database migration 
FastAPI backend for custom logic 
React dashboard with chat interface 
Direct ERP/WMS API integrations 
Multi-tenant support 
Role-based access control (RBAC) 
 

⚙️ Configuration 

Environment Variables / n8n Credentials 

Credential 
Where to Set 
Required 
ANTHROPIC_API_KEY 
n8n Credentials → Anthropic 
✅ Yes 
GOOGLE_SHEETS_OAUTH 
n8n Credentials → Google Sheets 
✅ Yes 
GMAIL_OAUTH 
n8n Credentials → Gmail 
✅ Yes 
SLACK_OAUTH 
n8n Credentials → Slack 
Optional 
Customizing Agent Behavior 

Each agent's behavior is controlled by its system prompt in the prompts/ folder. You can customize: 

Thresholds: What counts as "low stock" or "high risk" 
Weights: How supplier scores are calculated 
Tone: Formal vs. conversational briefing style 
Actions: What the agent recommends vs. auto-executes 
Output format: JSON structure, report layout 
 

💰 Cost Estimate 

Component 
Monthly Cost 
n8n Cloud (Starter) 
~$24 
Claude API (Sonnet, ~500 calls/day) 
~$30–60 
Google Workspace 
Free 
Slack 
Free tier 
Total 
~$54–$85/month 
 

⚠️ Known Limitations 

Batch processing, not real-time — Workflows run on schedules (hourly/daily/weekly) 
Manual data entry — Someone must keep Excel files updated until ERP integration is added 
No custom UI — Outputs are emails, Slack, and Google Sheets (no web dashboard) 
LLM-based forecasting — Directional insights, not statistical precision; best for < 500 SKUs 
Single-user approvals — Basic email-link approval; no RBAC 
Scale ceiling — Designed for ~100–500 SKUs, 10–50 suppliers 
See docs/graduation_guide.md for when and how to scale beyond these limits. 

 

🤝 Contributing 

Contributions are welcome! Please see CONTRIBUTING.md for guidelines. 

How to Contribute 

Fork the repository 
Create a feature branch (git checkout -b feature/amazing-feature) 
Commit your changes (git commit -m 'Add amazing feature') 
Push to the branch (git push origin feature/amazing-feature) 
Open a Pull Request 
Areas We Need Help With 

📊 Statistical forecasting model integration (Prophet, ARIMA) 
🔌 ERP connector templates (SAP, Oracle, Odoo) 
🎨 Looker Studio dashboard templates 
📝 Prompt optimization for specific industries (FMCG, manufacturing, retail) 
🌐 Localization (multi-language support for briefings) 
🧪 Test datasets for different industries 
 

📄 License 

This project is licensed under the MIT License — see the LICENSE file for details. 

 

🙏 Acknowledgments 

n8n — Workflow automation platform 
Anthropic — Claude LLM 
Google Sheets API — Zero-cost persistent storage 
 

Built with ❤️ for supply chain teams who are tired of spreadsheet hell.  

Report Bug • Request Feature • Discussions 

 
