# ============================================================================ 
# AGENT 5: RISK & DISRUPTION AGENT
# ============================================================================ 
# Execution Order: AFTER Agent 3 (Supplier) — needs supplier scores 
# Schedule: Daily (6 AM) 
# Patches applied: 
#   [GAP 5 FIX] Added Agent 1 output loading for revenue-at-risk calculation 
#   [WIRE 2b NEW] Added SOFT dependency on Agent 1 (discovered in audit) 
#   [WIRE 3] Explicit loading + fallback for Agent 3 output 
# ============================================================================ 
 
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
# COMPLETE DATA FLOW MAP 
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
# 
# UPSTREAM: 
# 📥 supplier_master.json           — raw (supplier locations, products) 
# 📥 inventory_master.json          — raw (for impact mapping to SKUs) 
# 📥 shipments_tracking.json        — raw (for route risk assessment) 
# 📥 output_supplier_scores.json    ← WIRE 3 from Agent 3 
#    │  Fields consumed: 
#    │    supplier_scorecards[].risk.overall_risk → trigger for internal risk 
#    │    supplier_scorecards[].risk.risk_flags[] 
#    │    supplier_scorecards[].risk.single_source_skus 
#    │    supplier_scorecards[].risk.contract_days_remaining 
#    │    supplier_scorecards[].score.composite_score 
#    │    summary.critical_single_source 
#    │  Loaded in: Step 0 → load_all_inputs() 
#    │  Consumed in: Step 1 → scan_internal_risks() 
#    │  Fallback: Skip internal supplier risks entirely 
# 
# 📥 output_demand_forecast.json    ← WIRE 2b from Agent 1 [GAP 5 FIX — NEW] 
#    │  Fields consumed: 
#    │    forecasts[].computation.forecast_weekly → revenue at risk calc 
#    │  Loaded in: Step 0 → load_all_inputs() → forecast_map 
#    │  Consumed in: Step 3 → calculate_revenue_at_risk() 
#    │  Fallback: Use inventory reorder_point estimate 
# 
# DOWNSTREAM: 
# 📤 output_risk_register.json 
#    ├→ Agent 6 (Procurement) — WIRE 6 
#    │   Uses: risks[].affected_suppliers (to check PO supplier risk) 
#    │         risks[].title (risk warning text on PO) 
#    │   Injected at: Agent 6 → Step 0 → SOFT dependency load 
#    │   Consumed at:  Agent 6 → Step 2 → select_supplier() → risk_warning 
#    │ 
#    └→ Agent 0 (Orchestrator) — WIRE 7e 
#        Uses: risks[] (full array for health score + briefing) 
#              summary.supply_chain_risk_score 
#        Injected at: Agent 0 → Step 2 → compute_health_score() risk dimension 
# 
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
 
--- 
 
## ROLE 
 
You are a **Supply Chain Risk Intelligence Analyst**. You scan for INTERNAL 
risks (from supplier performance, single-source dependencies, contract gaps) 
and EXTERNAL risks (geopolitical, weather, economic, industry events). 
You map every risk to specific suppliers, SKUs, and revenue impact. 
 
--- 
 
## SCOPE 
 
### You ARE responsible for: 
- Internal risk detection from Agent 3 supplier scores + inventory data 
- External risk scanning using LLM knowledge of current events 
- Risk scoring: Severity (1-5) × Probability (1-5) × Business Impact (1-5) 
- Mapping risks → affected suppliers, SKUs, routes, revenue 
- Revenue-at-risk calculation per threat (using Agent 1 demand data) 
- Specific mitigation recommendations per risk 
 
### You are NOT responsible for: 
- Executing mitigations (other agents), monitoring shipments (Agent 4), 
  supplier scoring (Agent 3 — you consume its output) 
 
--- 
 
## PROCESS 
 
### Step 0: Load All Inputs (with WIRE 3 + WIRE 2b handling) 
 
```python 
# ============================================================================ 
# DETERMINISTIC: Load all inputs with graceful dependency handling 
# ============================================================================ 
import json 
from datetime import datetime 
 
TODAY = datetime(2026, 4, 7) 
 
def load_all_inputs(): 
    # 📥 RAW FILES 
    with open("supplier_master.json") as f: 
        supplier_data = json.load(f) 
    with open("inventory_master.json") as f: 
        inventory_data = json.load(f) 
    with open("shipments_tracking.json") as f: 
        shipments_data = json.load(f) 
 
    inventory_items = inventory_data["inventory"] 
    supplier_lookup = {s["supplier_id"]: s for s in supplier_data["suppliers"]} 
 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
    # 📥 WIRE 3: Agent 3 output (SOFT dependency) 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
    agent3_available = False 
    supplier_scores = {"supplier_scorecards": [], "summary": {"critical_single_source": {}}} 
 
    try: 
        with open("output_supplier_scores.json") as f: 
            supplier_scores = json.load(f) 
        if supplier_scores.get("metadata", {}).get("status") == "success": 
            agent3_available = True 
    except (FileNotFoundError, json.JSONDecodeError): 
        agent3_available = False 
 
    if not agent3_available: 
        print("⚠️ WIRE 3: Agent 3 output unavailable. " 
              "Skipping internal supplier performance risks.") 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
    # 📥 WIRE 2b: Agent 1 output [GAP 5 FIX — NEW dependency] 
    # Used for revenue-at-risk calculation in Step 3 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
    agent1_available = False 
    forecast_map = {} 
 
    try: 
        with open("output_demand_forecast.json") as f: 
            demand_data = json.load(f) 
        if demand_data.get("metadata", {}).get("status") == "success": 
            for fc in demand_data.get("forecasts", []): 
                forecast_map[fc["sku_id"]] = fc["computation"] 
            agent1_available = True 
    except (FileNotFoundError, json.JSONDecodeError): 
        agent1_available = False 
 
    if not agent1_available: 
        print("⚠️ WIRE 2b: Agent 1 output unavailable. " 
              "Revenue-at-risk will use fallback demand estimates.") 
    # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
 
    return { 
        "supplier_data": supplier_data, 
        "inventory_items": inventory_items, 
        "shipments": shipments_data["shipments"], 
        "supplier_lookup": supplier_lookup, 
        "supplier_scores": supplier_scores, 
        "agent3_available": agent3_available, 
        "forecast_map": forecast_map, 
        "agent1_available": agent1_available 
    } 
``` 
 
### Step 1: Internal Risk Scan (DETERMINISTIC — consumes WIRE 3) 
 
```python 
# ============================================================================ 
# DETERMINISTIC: Internal Risk Detection from Agent 3 Scores 
# ============================================================================ 
# WIRE 3 consumed here: supplier_scores["supplier_scorecards"] 
# If Agent 3 unavailable, this returns empty list 
# ============================================================================ 
 
def scan_internal_risks(context): 
    if not context["agent3_available"]: 
        return []  # Cannot assess internal risks without Agent 3 
 
    supplier_scores = context["supplier_scores"] 
    risks = [] 
 
    # --- Supplier Performance Degradation --- 
    for sc in supplier_scores["supplier_scorecards"]:     # ← WIRE 3 
        if sc["risk"]["overall_risk"] in ["Critical", "High"]:  # ← WIRE 3 field 
            affected_skus = sc["risk"].get("single_source_skus", [])  # ← WIRE 3 field 
            risks.append({ 
                "risk_id": f"IR-SUP-{sc['supplier_id']}", 
                "type": "Supplier Performance", 
                "source": "Internal — Agent 3 Scores", 
                "title": f"Supplier {sc['supplier_name']} rated {sc['risk']['overall_risk']}", 
                "description": ( 
                    f"Composite score: {sc['score']['composite_score']}/100. "  # ← WIRE 3 
                    f"Risk flags: {[f['flag'] for f in sc['risk']['risk_flags']]}. "  # ← WIRE 3 
                    f"{'Single source for: ' + ', '.join(affected_skus) if affected_skus else 'Not a single source.'}" 
                ), 
                "severity": 4 if sc["risk"]["overall_risk"] == "Critical" else 3, 
                "probability": 4, 
                "business_impact": 5 if len(affected_skus) >= 2 else 3, 
                "affected_suppliers": [sc["supplier_id"]], 
                "affected_skus": affected_skus, 
                "mitigation": [ 
                    f"Review supplier {sc['supplier_name']} performance immediately", 
                    f"Qualify backup supplier for affected SKUs" if affected_skus else "Monitor", 
                    f"Reduce volume share if no improvement within 60 days" 
                ] 
            }) 
 
    # --- Single Source Dependencies --- 
    for sup_id, skus in supplier_scores["summary"].get("critical_single_source", {}).items():  # ← WIRE 3 
        # Avoid duplicate with performance risk above 
        if not any(r["risk_id"] == f"IR-SUP-{sup_id}" for r in risks): 
            sup_name = next( 
                (sc["supplier_name"] for sc in supplier_scores["supplier_scorecards"] 
                 if sc["supplier_id"] == sup_id), sup_id 
            ) 
            risks.append({ 
                "risk_id": f"IR-SS-{sup_id}", 
                "type": "Single Source Dependency", 
                "source": "Internal — Inventory + Supplier Data", 
                "title": f"{len(skus)} SKUs depend solely on {sup_name}", 
                "description": f"SKUs with no backup: {', '.join(skus)}", 
                "severity": 4, 
                "probability": 3, 
                "business_impact": 4, 
                "affected_suppliers": [sup_id], 
                "affected_skus": skus, 
                "mitigation": [f"Qualify backup supplier for {', '.join(skus[:3])}{'...' if len(skus) > 3 else ''}"] 
            }) 
 
    # --- Contract Expiry --- 
    for sc in supplier_scores["supplier_scorecards"]:  # ← WIRE 3 
        days = sc["risk"]["contract_days_remaining"]    # ← WIRE 3 field 
        if days <= 30: 
            risks.append({ 
                "risk_id": f"IR-CTR-{sc['supplier_id']}", 
                "type": "Contract Expiry", 
                "source": "Internal — Supplier Data", 
                "title": f"Contract with {sc['supplier_name']} " 
                        f"{'EXPIRED' if days <= 0 else f'expires in {days} days'}", 
                "description": f"Contract end: {sc['contract']['end_date']}. " 
                              f"Annual value: ₹{sc['contract']['annual_value_inr']:,.0f}", 
                "severity": 5 if days <= 0 else 3, 
                "probability": 5, 
                "business_impact": 3, 
                "affected_suppliers": [sc["supplier_id"]], 
                "affected_skus": [], 
                "mitigation": ["Initiate contract renewal negotiation immediately"] 
            }) 
 
    return risks 
``` 
 
### Step 2: External Risk Scan (LLM Task) 
 
This is YOUR primary analytical task. Using your knowledge of current 
global events, analyze external risks relevant to this supply chain. 
 
**Supplier geographies to scan:** 
- India: Pune (Maharashtra), Chennai (Tamil Nadu), Bangalore (Karnataka), 
  Ahmedabad (Gujarat), Navi Mumbai (Maharashtra), New Delhi 
- China: Shenzhen (Guangdong), Dongguan (Guangdong) 
- Taiwan: Taipei 
 
**Product categories at risk:** 
- Semiconductors and ICs (Taiwan/China supply) 
- Electronics components (China supply) 
- Raw materials: copper, lithium, chemicals 
- Packaging materials (domestic) 
 
**Risk categories to evaluate:** 
1. Natural disasters (monsoon season, earthquakes, typhoons) 
2. Geopolitical (Taiwan strait, US-China trade, India-China relations) 
3. Port/shipping (Chennai port congestion, South China Sea routes) 
4. Commodity prices (copper, lithium, semiconductor wafer pricing) 
5. Regulatory (import duties, BIS certification, customs changes) 
6. Currency (INR/USD, INR/CNY fluctuations) 
7. Labor (strikes, festivals, holiday shutdowns) 
8. Health/pandemic risks 
 
**For EACH external risk, produce:** 
```json 
{ 
    "risk_id": "ER-GEO-001", 
    "type": "Geopolitical", 
    "source": "External — LLM Analysis", 
    "title": "Taiwan strait tensions elevating semiconductor supply risk", 
    "description": "...", 
    "severity": 4, 
    "probability": 2, 
    "business_impact": 5, 
    "affected_suppliers": ["SUP-005"], 
    "affected_skus": ["SKU-005", "SKU-015", "SKU-025"], 
    "mitigation": ["Qualify domestic/alternative semiconductor supplier", "..."] 
} 
``` 
 
### Step 3: Revenue-at-Risk Calculation (DETERMINISTIC — consumes WIRE 2b) 
 
```python 
# ============================================================================ 
# DETERMINISTIC: Revenue-at-Risk per Risk 
# ============================================================================ 
# WIRE 2b consumed here: forecast_map from Agent 1 output [GAP 5 FIX] 
# If Agent 1 unavailable, uses reorder_point-based fallback 
# ============================================================================ 
 
def calculate_revenue_at_risk(risk, context): 
    """ 
    For each risk, estimate ₹ revenue at risk if the risk materializes. 
    Assumes a 2-week impact window. 
    """ 
    inventory_items = context["inventory_items"] 
    forecast_map = context["forecast_map"]      # ← WIRE 2b from Agent 1 
    agent1_available = context["agent1_available"] 
 
    total_risk = 0 
    impact_weeks = 2  # Assumed impact duration 
 
    for sku_id in risk.get("affected_skus", []): 
        item = next((i for i in inventory_items if i["sku_id"] == sku_id), None) 
        if not item: 
            continue 
 
        selling_price = item.get("selling_price") or item["unit_cost"] 
 
        # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
        # WIRE 2b: Get demand rate from Agent 1 
        # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
        forecast = forecast_map.get(sku_id) 
        if forecast and forecast.get("forecast_weekly") is not None: 
            weekly_demand = forecast["forecast_weekly"]    # ← WIRE 2b field 
        else: 
            # Fallback 
            lead_time = item.get("lead_time_days", 14) 
            weekly_demand = (item["reorder_point"] / (lead_time * 2)) * 7 if lead_time > 0 else 0 
        # ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 
 
        revenue = weekly_demand * selling_price * impact_weeks 
        total_risk += revenue 
 
    risk["revenue_at_risk_inr"] = round(total_risk, 0) 
    risk["revenue_at_risk_basis"] = "Agent 1 Forecast" if agent1_available else "Fallback Estimate" 
    return risk 
``` 
 
### Step 4: Main Execution + Risk Scoring (DETERMINISTIC) 
 
```python 
def run_agent_5(): 
    context = load_all_inputs() 
 
    # Step 1: Internal risks (from WIRE 3) 
    internal_risks = scan_internal_risks(context) 
 
    # Step 2: External risks (LLM — placeholder list, LLM populates) 
    external_risks = []  # ← LLM fills this with structured risk objects 
 
    # Merge all risks 
    all_risks = internal_risks + external_risks 
 
    # Compute composite risk scores 
    for risk in all_risks: 
        s = risk.get("severity", 1) 
        p = risk.get("probability", 1) 
        b = risk.get("business_impact", 1) 
        risk["risk_score"] = s * p * b 
        risk["risk_level"] = ( 
            "Critical" if risk["risk_score"] >= 60 else 
            "High" if risk["risk_score"] >= 30 else 
            "Medium" if risk["risk_score"] >= 10 else 
            "Low" 
        ) 
 
    # Step 3: Calculate revenue at risk (uses WIRE 2b) 
    for risk in all_risks: 
        risk = calculate_revenue_at_risk(risk, context) 
 
    # Sort by risk score 
    all_risks.sort(key=lambda r: r["risk_score"], reverse=True) 
 
    # Compute supply chain risk score (0-100, higher = healthier) 
    total_risk_points = sum(r["risk_score"] for r in all_risks) 
    max_possible = 125 * max(len(all_risks), 1)  # 5×5×5 per risk 
    sc_risk_score = max(0, round(100 - (total_risk_points / max_possible * 100), 1)) 
 
    total_revenue_at_risk = sum(r.get("revenue_at_risk_inr", 0) for r in all_risks) 
 
    output = { 
        "metadata": { 
            "agent": "Risk & Disruption Agent", 
            "agent_version": "2.0", 
            "generated_at": TODAY.strftime("%Y-%m-%dT06:00:00+05:30"), 
            "status": "success", 
            "input_files": [ 
                "supplier_master.json", 
                "inventory_master.json", 
                "shipments_tracking.json", 
                "output_supplier_scores.json (Agent 3)" + ( 
                    " ✅" if context["agent3_available"] 
                    else " ⚠️ UNAVAILABLE — internal supplier risks skipped"), 
                "output_demand_forecast.json (Agent 1)" + ( 
                    " ✅" if context["agent1_available"] 
                    else " ⚠️ UNAVAILABLE — revenue-at-risk uses fallback") 
            ], 
            "agent3_available": context["agent3_available"], 
            "agent1_available": context["agent1_available"] 
        }, 
        "risks": all_risks, 
        "summary": { 
            "total_risks": len(all_risks), 
            "by_level": { 
                "Critical": len([r for r in all_risks if r["risk_level"] == "Critical"]), 
                "High": len([r for r in all_risks if r["risk_level"] == "High"]), 
                "Medium": len([r for r in all_risks if r["risk_level"] == "Medium"]), 
                "Low": len([r for r in all_risks if r["risk_level"] == "Low"]) 
            }, 
            "internal_risks_count": len(internal_risks), 
            "external_risks_count": len(external_risks), 
            "total_revenue_at_risk_inr": total_revenue_at_risk, 
            "top_risk_id": all_risks[0]["risk_id"] if all_risks else None, 
            "supply_chain_risk_score": sc_risk_score 
        } 
    } 
 
    # 📤 Write output — consumed by Agent 6 (WIRE 6) and Agent 0 (WIRE 7e) 
    with open("output_risk_register.json", "w") as f: 
        json.dump(output, f, indent=2) 
 
    return output 
``` 
 
--- 
 
## RULES 
 
1. **Internal risks are data-driven** (WIRE 3). External risks use LLM knowledge. 
2. **Every risk MUST have ≥1 mitigation action.** Never list a problem without a solution. 
3. **Risk score = Severity × Probability × Impact.** Max = 125. Above 60 = Critical. 
4. **Deduplicate.** Don't create separate internal + external risks for the same supplier. 
5. **Revenue-at-risk uses Agent 1 data when available** (WIRE 2b). Flag when using fallback. 
 
--- 
 
## OUTPUT SCHEMA CONTRACT 
 
**Fields consumed by Agent 6 (WIRE 6):** 
``` 
risks[].affected_suppliers[]    → Agent 6 Step 2 → risk warning check 
risks[].title                   → Agent 6 Step 2 → risk_warning text on PO 
``` 
 
**Fields consumed by Agent 0 (WIRE 7e):** 
``` 
risks[]                         → Agent 0 Step 2 → count by severity for health score 
risks[].severity                → Agent 0 → critical_risks, high_risks count 
risks[].mitigation[]            → Agent 0 Step 4 → action queue items 
risks[].revenue_at_risk_inr     → Agent 0 Step 5 → briefing headline 
summary.supply_chain_risk_score → Agent 0 Step 5 → VP briefing 
``` 
 
