![](Diagrams/Architecture/architecture.png)

# 🚀 Azure End-to-End Data Engineering Project

## Medallion Architecture with ADF, Databricks & ADLS Gen2

### 📌 Project Overview
This project implements a full end-to-end Azure data engineering platform using modern best practices and the **Medallion Architecture (Bronze → Silver → Gold)**.

The solution ingests data from:
- 🌐 Rebrickable API (cloud REST API)
- 🗄️ Local PostgreSQL (DVD Rentals – Pagila dataset) via Self-Hosted Integration Runtime

The platform processes data using:
- Azure Data Factory for orchestration and ingestion
- Azure Data Factory Mapping Data Flows for Silver-layer transformations
- Azure Databricks + Delta Lake for advanced processing and Gold-layer modeling
- Azure Data Lake Storage Gen2 as the central data lake
- Azure Key Vault for secrets management
- GitHub for version control and collaboration

The final output exposes analytics-ready Gold tables suitable for BI, reporting, and downstream consumption.

### 🏗️ Architecture
High-level architecture:
1. Source systems (API + PostgreSQL)
2. ADF ingestion pipelines
3. ADLS Gen2 (Bronze, Silver, Gold containers)
4. Databricks transformation layer
5. Delta Lake tables
6. GitHub-integrated CI-style workflow


### 🧱 Medallion Architecture Design

#### 🥉 Bronze – Raw Ingestion
**Purpose:**  
Store data exactly as received, without transformation.

**Sources:**
- Rebrickable REST API (JSON)
- PostgreSQL Pagila DVD rental database

**Characteristics:**
- Append-only
- Source-aligned
- No business logic

---

#### 🥈 Silver – Clean & Conformed
**Purpose:**  
Standardize, clean, deduplicate, and type data.

**Implemented using:**
- ADF Mapping Data Flows (DVD Rentals)
- Databricks notebooks (Rebrickable)

**Transformations include:**
- Data type enforcement
- Column renaming and standardization
- Null handling
- Deduplication using window functions
- Derived business attributes

---

#### 🥇 Gold – Business & Analytics Layer
**Purpose:**  
Provide business-ready, modeled, and aggregated datasets.  
Implemented fully in Databricks using Delta Lake.

**Rebrickable Gold Tables:**
- `gold.dim_minifigs`  
  Curated LEGO minifigure dimension.  
  Includes:
  - Surrogate key
  - Business attributes
  - Audit timestamps
  - Derived analytics columns:
    - superhero flag
    - name length
    - modified year

- `gold.fact_minifigs_stats`  
  Snapshot analytics fact table.  
  Includes:
  - snapshot date
  - total minifigs
  - average parts
  - min / max parts
  - superhero count

**DVD Rentals Gold Tables:**  
Star-schema style model:
- `gold.dim_customer`
- `gold.dim_film`
- `gold.fact_rentals`

Built from cleaned silver tables using joins, derivations, and filtering.


---

### ⚙️ Technology Stack
- Azure Data Factory
- Azure Databricks
- Azure Data Lake Storage Gen2
- Delta Lake
- Azure Key Vault
- Azure Entra ID (Service Principal)
- GitHub integration
- Self-Hosted Integration Runtime (on-prem PostgreSQL)

---

### 🔐 Security & Best Practices
- Secrets stored in Azure Key Vault
- Databricks authentication using Service Principal OAuth
- No secrets committed to GitHub
- ADLS access controlled via IAM RBAC
- SHIR used for secure on-prem connectivity

---

### 🔁 Data Engineering Workflow
1. Ingest API and PostgreSQL data with ADF
2. Store raw data in Bronze container
3. Clean and standardize into Silver
4. Transform and model in Databricks
5. Write curated Delta tables to Gold
6. Version all assets in GitHub

---

### 🗂️ Repository Structure

```text
azure-data-engineering-project/
├── Azure Data Factory/
│   ├── pipelines/
│   ├── dataflows/
│   ├── datasets/
│   ├── linkedServices/
│   └── triggers/
├── databricks/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── architecture/
│   ├── diagrams/
│   └── screenshots/
├── infra/
│   └── resource-list.md
└── README.md
```


---

### 🧪 Key Engineering Features Demonstrated
- REST API ingestion
- On-prem PostgreSQL ingestion using SHIR
- Medallion architecture
- Mapping Data Flows
- Delta Lake
- Slowly evolving datasets
- Star schema modeling
- Snapshot fact tables
- Secure secret handling
- Git-integrated ADF
- Databricks (Pyspark)


---

### ▶️ How to Run the Project
1. Deploy Azure resources
2. Configure Key Vault secrets
3. Connect ADF to GitHub
4. Configure SHIR
5. Trigger Bronze pipelines
6. Run Silver transformations in ADF
7. Execute Databricks Gold notebooks
8. Validate Gold Delta tables

---

### 🎯 Learning Outcomes
This project demonstrates the ability to:
- Design cloud data platforms
- Implement medallion architecture
- Build production-style ingestion pipelines
- Apply data modeling concepts
- Secure enterprise data systems
- Version control data engineering assets
- Work with both cloud and on-prem data
- Databricks mastery

---

### 👤 Author
**[Ahmad Olaitan Alege]**  
 2026


