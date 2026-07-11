# 💊 Pharma Risk Analytics: Drug Shortage & Chemical Property Mapping Model

An advanced Power BI analytics solution that bridges the gap between regulatory pharmaceutical supply chains, chemical data science, and financial market trends. This model maps FDA drug shortages against molecular descriptors and stock performance to uncover systemic vulnerabilities in the therapeutic supply chain.

---

## 📖 Project Overview

Traditional supply chain risk management relies heavily on lagging logistical indicators. This project introduces a novel framework by merging **three distinct data domains** to proactively identify systemic manufacturing and market vulnerabilities:

1. **Regulatory Risk (`fda shortage`):** Tracks real-time and historical FDA drug shortage events, identifying the current status of a drug (e.g., *Current* vs. *To Be Discontinued*), initial posting dates, manufacturers, and therapeutic categories.
2. **Chemical Data Science (`cluster output` & `cluster summary`):** Ingests molecular data from the ChEMBL database, profiling compounds based on physical descriptors such as molecular weight, partition coefficient ($logP$), hydrogen bond donors ($HBD$), and hydrogen bond acceptors ($HBA$). Using **UMAP (Uniform Manifold Approximation and Projection)** dimensional reduction, similar molecules are clustered together spatially to see if specific chemical structures suffer disproportionate manufacturing bottlenecks.
3. **Market Economics (`stock data`):** Integrates time-series financial index data alongside vendor stock variations to establish how market pressures correlate with or predict supply interruptions.

> 💡 **The Core Insight:** By pairing molecular geometry with supply chain data, this model helps procurement teams and pharmaceutical analysts shift from reactive crisis management to structure-aware risk mitigation—isolating vulnerable compound clusters before supply chain failures impact the market.

---

## 🏗️ Data Model Architecture

The underlying data infrastructure relies on a highly optimized Power BI Tabular Model (**Compatibility Level 1600**) built on top of a hybrid star/snowflake schema designed for sub-second cross-filtering and complex DAX calculations.

### Data Schema Relationship Map
### Table Dictionary

| Table Name | Type | Description | Key Fields |
| :--- | :--- | :--- | :--- |
| **`fda shortage`** | Fact / Dim | Logs operational records of supply chain failures and regulatory statuses. | `shortage_flag`, `company_name`, `therapeutic_category`, `status` |
| **`cluster output`** | Dimension | Contains the data-science layer, mapping unique ChEMBL IDs to UMAP coordinates and raw molecular properties. | `molecule_chembl_id`, `umap_x`, `umap_y`, `molecular_weight` |
| **`cluster summary`**| Aggregation | Pre-calculated statistical baselines per structural group for fast benchmarking. | `mean_mw`, `mean_logp`, `mean_hba`, `mean_hbd` |
| **`shortage match`** | Bridge | A multi-key resolution table matching specific regulatory shortage logs to unique molecular clusters. | Composite keys linking logs to ChEMBL IDs. |
| **`stock data`** | Fact | Tracks timeline-driven financial trends and vendor stock variations across historical dates. | `date`, `stock_price`, `ticker` |
| **`PaddedDateTableDates`** | Dimension | Continuous calendar dimension supporting advanced DAX Time-Intelligence operations. | `Date`, `Year`, `Quarter`, `Month` |

---

## 🚀 Key Features & Analytical Views

* **Chemical Cluster Explorer:** A scatter plot layout graphing `umap_x` vs. `umap_y` where each dot represents a drug compound. Color-coded by shortage flags to immediately pinpoint high-risk structural pockets.
* **Supply Lifecycle Timeline:** Chronological tracking of `To Be Discontinued` versus active shortages over time against company names and market performance indicators.
* **Molecular Profile Analysis:** Deep dive into whether specific chemical thresholds (e.g., high molecular weight or extreme $logP$ values) show a higher statistical correlation with prolonged shortage durations.
* **Time-Intelligence Alignment:** Synchronized tracking of stock market volatility dips right before or during major manufacturing shortage announcements.

---

## 🛠️ Technical Configurations

* **BI Platform:** Microsoft Power BI Desktop
* **Analysis Services Engine:** Tabular Metadata
* **Language Locale:** English (US / `1033`)
* **Optimization:** Includes pre-aggregated cluster tables to drastically reduce RAM overhead during runtime UMAP rendering.

---
