# 📊 NovaTech Revenue Intelligence Dashboard & AI Integration

## 📌 Project Overview
As a Business Intelligence Analyst at NovaTech, I was tasked by the VP of Revenue Operations, Sarah Chen, to eliminate the manual extraction of weekly reports across siloed tools. The objective was to unify the company's revenue data—spanning marketing, sales, and customer support—into a single interactive dashboard and an AI-powered natural language semantic layer. 

> **Note on Data Privacy:** The raw datasets (CRM Deals, Marketing Campaigns, and Support Tickets) used in this project are proprietary and not included in this repository. However, the methodology, data engineering logic, and business insights are fully documented below.

## 🛠 Tech Stack
* **Business Intelligence:** AWS QuickSight
* **Data Engine:** SPICE (Super-fast, Parallel, In-memory Calculation Engine)
* **Generative BI & AI:** Amazon Q (Semantic Layer & Natural Language Querying)
* **Data Engineering (No-Code ETL):** Full Outer Joins, Level-Aware Calculations (LAC), Data Type Casting

## 🧠 Technical Challenges & Solutions
Unifying three disparate domains (Marketing, Sales, CRM) presented significant data grain challenges:

1. **Handling Orphan Records via Full Outer Joins:** 
   To ensure "orphan" marketing leads and support tickets (those without a corresponding CRM account) were not dropped from the analysis, I engineered a unified dataset using a Full Outer Join on the `account_id`.
2. **Solving the Cartesian Product (Row Inflation):** 
   The Full Outer Join altered the data grain, duplicating rows for every ticket and campaign associated with a single account (e.g., inflating a baseline of 3,000 support tickets to 63,624 rows). 
   * *Solution:* I protected the dashboard's integrity by implementing **Count Distinct** aggregations for entity counts (leads, tickets) and utilizing advanced **Level-Aware Calculations (LAC)**. This ensured that metrics like Campaign ROI aggregated unique values before division, preventing duplicated marketing spend from distorting financial KPIs.
3. **AI Semantic Enrichment (Amazon Q):** 
   Initially, the baseline AI struggled with domain-specific terminology (e.g., failing to link "revenue" to `deal_value`) and blindly summed duplicated join rows. I applied Semantic Enrichment by mapping synonyms ("client", "revenue") and correctly formatting data types, significantly improving the AI's natural language comprehension.

## 💡 Key Business Insights
By leveraging cross-sheet navigation and one-click filtering, the unified dashboard uncovered three critical business interventions:

* **📉 Marketing Efficiency:** The Paid Social channel generates 35% of all leads but yields a negative ROI of -12% when calculating aggregated spend versus revenue. 
  * *Action:* Reallocate 20% of the Paid Social budget to Organic Search.
* **⚔️ Product Competitiveness:** The primary loss reason for the Enterprise segment is "Competitor Won" (accounting for 45% of lost deals). Our flagship product (NovaPulse Ultimate) is losing its competitive edge. 
  * *Action:* Conduct an immediate gap analysis of missing features.
* **🚨 Churn Risk Identification:** 5 Enterprise accounts with a Deal Value >$20,000 have a "negative" customer sentiment and more than 10 open tickets recorded in the active system. 
  * *Action:* Customer Success Management to schedule alignment calls within 48 hours to prevent severe revenue churn.

## 📂 Repository Structure
Since the raw data cannot be shared, this repository contains the core analytical artifacts:
* `reports/NovaTech_Executive_Report.pdf` - The final 3-page strategic memo delivered to the VP of Revenue.
* `reports/Dashboard_Final_Export.pdf` - The exported visualizations (Marketing Funnel, Sales Pipeline, Customer Health) showcasing custom annotations and KPI summaries.
* `logs/16_Q_Exploration_Log.md` - Documentation of the Amazon Q semantic training, comparing the AI's responses against the dashboard's "Single Source of Truth".
* `logs/7a_verification_log.md` - The initial Data Quality and verification checks performed on the baseline CSVs.
* `Images/` - Selected screenshots demonstrating the Full Outer Join configuration, LAC formulas, and Amazon Q Semantic setup.
