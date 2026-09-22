# NYC Rodent Complaint & Restaurant Inspection Analysis

## Team Members

Samiha Zaman, Arooj Manzar

## The Question
When a New Yorker sees a rat, they call 311. When the Health Department inspects a restaurant, every violation gets a code. Both records are public. Nobody has told you whether they agree.

**Deliverable:** a Service Gap Index for every ZIP code in New York City, and a dashboard where anyone can type in their own ZIP and find out how their block is served.

## Project Overview

This project analyzes the gap between what NYC residents report about rodent activity (311 complaints) and what NYC Department of Health inspectors actually verify during restaurant inspections. By joining these two datasets at the ZIP-code level, we identify neighborhoods where inspector-verified rodent evidence diverges from resident-reported complaints — helping surface potential underreporting or service delivery gaps.

The project was built entirely in **Databricks** using SQL notebooks, AI/BI Dashboards, and a Genie AI agent, and covers data from January 2025 through September 2026.

---

## Data Sources

- **NYC 311 Rodent Complaints** — 50,954 records of resident-reported rodent sightings and conditions attracting rodents, including location type, ZIP code, borough, and complaint resolution timestamps.
- **NYC DOHMH Restaurant Inspections** — 158,083 restaurant inspection violation records from the NYC Department of Health and Mental Hygiene, including violation codes, inspection scores, grades, and restaurant identifiers.

---

## Project Components

### 1. SQL Data Pipeline Notebook

The notebook follows a three-block structure:

- **Block One — Data Profiling & Auditing:** Comprehensive quality checks on both raw datasets, including null audits, duplicate detection, invalid and out-of-state ZIP code identification, constant column detection, categorical spelling variant discovery, and date range validation.

- **Block Two — Cleaning & Joining:** Transformation of raw tables into analysis-ready tables with standardized 5-digit ZIP codes, deduplication, categorical harmonization, and rodent-evidence flagging. A gold analytics table (`zip_service_gap`) joins the two datasets at the ZIP-code level using multi-CTE SQL pipelines with window functions, z-score normalization, and a tiered data-sufficiency classification system (sufficient / thin / insufficient).

- **Block Three — Analysis & Refinement:** Critical analysis of the metrics, including correlation testing between complaint volume and restaurant count, decile-based ranking comparisons, and refinement of the service gap index into two population-matched metrics: a **Restaurant Service Gap Index** (commercial complaints vs. verified restaurant rodent evidence) and a **Residential Complaint Rank** (citywide ranking of residential complaint volume with no restaurant denominator).

### 2. NYC Service Gap Dashboard (AI/BI)

An interactive dashboard with:
- A global ZIP-code filter for drill-down exploration
- KPI counters: Service Gap Index, 311 Complaints, Restaurants Inspected, Verified Rodent Rate
- Bar charts: 311 Complaint Breakdown, Inspection Findings, Z-Score Comparison, Key Rates
- Data tables: ZIP Code Details and Data Sufficiency Notes
- Contextual narrative explaining methodology and data-sufficiency caveats for non-technical stakeholders

### 3. Genie AI Agent

A natural-language Q&A agent grounded in the cleaned Unity Catalog tables, enabling users to ask questions about:
- Rodent complaint patterns by ZIP code and borough
- Restaurant inspection findings and verified rodent rates
- Service gap index rankings with data-sufficiency filtering
- Comparison of resident-reported complaints vs. inspector-verified evidence

---

## Key Findings

- 311 rodent complaints are overwhelmingly residential (~96%), originating from apartment buildings, dwellings, sidewalks, and vacant lots — not commercial buildings or restaurants.
- Restaurant inspection rodent evidence and 311 complaint volume are uncorrelated (r = −0.03), confirming that the two datasets measure different populations and should not be combined into a single composite score without population-matched denominators.
- The final analysis splits measurement into two valid, independently scoped metrics to avoid misleading conclusions.

---

## Tech Stack

- **Platform:** Databricks (Unity Catalog, SQL Warehouses, Serverless Compute)
- **Languages:** SQL (Databricks SQL)
- **Visualization:** Databricks AI/BI Dashboards
- **AI/ML:** Databricks Genie (AI data-room agent)
- **Data Storage:** Unity Catalog managed tables

---
