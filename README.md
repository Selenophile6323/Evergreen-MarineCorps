# Optimizing Logistics Through Data Intelligence
### A Unified Data Architecture for Evergreen Marine Corp

## Overview
Evergreen Marine Corp, a global logistics and shipping company, manages data from
many disconnected sources — shipping ports, warehouses, delivery fleets, customs,
and currency exchanges. Relying on siloed or delayed information leads to shipment
delays, higher costs, poor routing, and missed revenue. This project designs a unified,
cloud-based data architecture to integrate operational, transactional, IoT, and
external data in real time, turning scattered data into centralized intelligence.

## Objectives
- Optimize delivery routing by 20% within 6 months (fuel use and delivery time)
- Achieve 95% accuracy in financial tracking by Q4 (<5% deviation in profitability analysis)
- Deploy real-time Power BI KPI dashboards for fleet, driver, and delivery performance
- Benchmark driver and fleet performance monthly via automated reports
- Enable secure external data sharing with clients and partners by end of year

## Data Sources
| Source | Nature | Format |
|---|---|---|
| Scraping Data | Carrier sites, weather, traffic, competitor data | JSON, HTML, CSV, web stream |
| In-House Data | Vehicle assignments, maintenance logs, route schedules | SQL (relational) |
| Website Transaction Data | Orders, payments, billing | SQL / NoSQL |
| IoT Database | GPS trackers, onboard sensors, telemetry | JSON, CSV, time-series |
| Currency Conversion Database | Foreign exchange rates | JSON, XML, SQL |

## Data Sinks
- **Revenue System** — real-time financial tracking and profitability analysis
- **Route Intelligence** — dynamic route optimization using IoT, fleet, and external data
- **Dashboard Reports** — Power BI dashboards consolidating all sources for cross-departmental KPIs
- **Ship Performance Report** — fleet/driver benchmarking (idle time, fuel use, SLA compliance)
- **External Data Sharing** — secure API/file sharing with clients and partners

## Cloud Architecture
Designed on Azure using a **Lakehouse architecture** (Bronze–Silver–Gold), combining
data lake and data warehouse patterns into a single, unified platform:

- **Ingestion:** Azure Data Factory (batch/ETL), Azure IoT Hub (real-time telemetry)
- **Bronze (raw):** Azure Data Lake Gen2, Blob Storage
- **Silver (cleaned):** Delta Lake — standardized, ACID-compliant datasets
- **Gold (curated):** Azure Synapse Analytics — business-ready data for reporting and ML
- **Transformation:** Azure Synapse Analytics (SQL + Spark)
- **Streaming:** Azure Stream Analytics, Azure Functions
- **Consumption:** Power BI dashboards, ML models
- **Data Sharing:** Azure Share — governed, policy-driven external access

## Pipeline Design
- **Batch ingestion (Bronze → Silver):** transaction, scraping, in-house, and currency
  data land in Bronze, then are cleaned and standardized into Silver
- **Stream ingestion (Bronze → Gold):** IoT/GPS data streams in and is transformed
  immediately for real-time reporting
- **Silver layer:** review, validate, clean, and enrich raw data
- **Gold layer:** identify KPIs, select key metrics, restructure for BI tools, visualize

## Pipeline Failure Strategy
A retry/fault-tolerance workflow ensures reliability:
1. Pipeline job executes a data task
2. On failure, retries up to 3 times with a 10-minute cool-off between attempts
3. If retries are exhausted, an alert is sent to the admin and the pipeline is marked failed

This ensures transient issues self-recover, admins are alerted only when necessary,
and failed runs are logged rather than allowed to push partial/corrupted data forward.

## Key Benefits
- **Modular:** clear separation between ingestion, storage, transformation, consumption
- **Scalable:** cloud-native services scale on demand
- **Flexible:** supports both batch and streaming data
- **Governed:** Delta Lake + Synapse support data integrity and auditing

## Author
Ramya Ramesh — Southern Alberta Institute of Technology
