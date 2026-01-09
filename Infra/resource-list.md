# 📦 Azure Resource Inventory – Data Engineering Project

This document lists all Azure resources deployed for this project, their purpose, and how they fit into the overall architecture.

---

## 🗂️ Resource Group
### 🔹 Resource Group
**Name:** `DE_Project1`  
**Purpose:** Logical container for all services related to this data engineering platform.

---

## 💾 Storage
### 🔹 Azure Data Lake Storage Gen2
**Name:** `deproj1adls`  
**Purpose:** Central data lake for Bronze, Silver, and Gold layers.

**Containers:**
- `bronze` – raw ingested data
- `silver` – cleansed, standardized datasets
- `gold` – analytics-ready curated tables

**Used by:**
- Azure Data Factory
- Azure Databricks
- Delta Lake

---

## 🔁 Orchestration
### 🔹 Azure Data Factory
**Name:** `adf-deproj1`  
**Purpose:** Data ingestion and orchestration layer.

**Responsibilities:**
- Ingest Rebrickable REST API data
- Ingest PostgreSQL data via SHIR
- Load raw data into Bronze
- Execute Mapping Data Flows for Silver layer

**Key features used:**
- REST connectors
- PostgreSQL connectors
- Mapping Data Flows
- Self-hosted Integration Runtime
- GitHub integration

---

## 🧮 Processing
### 🔹 Azure Databricks Workspace
**Name:** `adb-deproj1-ws`  
**Purpose:** Advanced transformation and analytics processing.

**Responsibilities:**
- Transform Silver → Gold
- Build dimension and fact tables
- Delta Lake management
- Data modeling
- Derived business metrics

**Technologies:**
- Apache Spark
- Delta Lake
- Databricks Repos
- Service Principal authentication

---

## 🏃 Integration
### 🔹 Self-hosted Integration Runtime (SHIR)
**Installed on:** Local machine  
**Purpose:** Secure connectivity between Azure Data Factory and on-prem PostgreSQL.

**Used for:**
- DVD Rentals (Pagila) dataset ingestion

---

## 🔐 Security
### 🔹 Azure Key Vault
**Name:** `kv-deproj1`  
**Purpose:** Secure secrets management.

**Secrets stored:**
- Rebrickable API key
- Service principal client secret
- Storage OAuth credentials

**Used by:**
- Azure Data Factory
- Azure Databricks

### 🔹 Microsoft Entra ID (Azure AD)
**Objects created:**
- Service principal (App Registration)

**Purpose:**
- OAuth authentication from Databricks to ADLS
- Secure, passwordless data access design

---

## 📂 Source Control
### 🔹 GitHub Repository
**Name:** `Azure-Data-Factory-and-Databricks-Project`  
**Purpose:** Version control and collaboration.

**Tracks:**
- ADF pipelines and data flows
- Databricks notebooks
- Architecture diagrams
- Documentation

**Integrated with:**
- Azure Data Factory Git mode
- Databricks Repos

---

## 🗄️ Data Sources
### 🔹 Rebrickable API
**Type:** Cloud REST API  
**Purpose:** LEGO minifig dataset ingestion.

### 🔹 PostgreSQL (LocalHost)
**Dataset:** Pagila DVD Rentals  
**Purpose:** Relational transactional dataset for dimensional modeling.

---

## 🏗️ Architectural Role Summary
| Resource | Role |
|----------|------|
| ADLS Gen2 | Central data lake |
| Azure Data Factory | Ingestion & orchestration |
| Databricks | Processing & modeling |
| Key Vault | Secrets & security |
| SHIR | Hybrid connectivity |
| GitHub | Version control |

---

## 📌 Notes
- All data layers are stored as Delta format
- No secrets are stored in code or GitHub
- Project follows medallion architecture
- Designed for portfolio and enterprise-style demonstration