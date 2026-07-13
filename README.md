# Pharma Risk Analytics

A Power BI analytics project that brings together pharmaceutical drug shortage records, molecular compound properties, chemical similarity clusters, and manufacturer market data to support exploratory supply-chain risk analysis.

## Project Overview

Pharmaceutical shortage information, molecular drug characteristics, and manufacturer market data are usually stored in separate systems. Reviewing these datasets independently makes it difficult to explore whether shortages are concentrated around specific manufacturers, therapeutic categories, molecular profiles, or time periods.

This project creates a unified Power BI environment where users can analyze drug shortage activity alongside ChEMBL molecular descriptors, UMAP-based chemical clusters, stock data, and time-based trends.

## Problem Statement

Drug shortages can interrupt treatment availability and create pressure on hospitals, procurement teams, manufacturers, and regulatory agencies.

The main analytical challenge is that shortage records describe supply events, while molecular databases describe chemical compounds and financial datasets describe company-level market activity. These datasets have different structures and levels of detail, so they cannot be compared directly without careful data modeling.

## Target Users

- Pharmaceutical supply-chain analysts
- Healthcare data analysts
- Drug procurement teams
- Regulatory researchers
- Pharmaceutical manufacturers
- Hospital inventory planners
- Business intelligence teams

## Business Questions

The dashboard is designed to help users explore questions such as:

- Which manufacturers appear most frequently in shortage records?
- Which therapeutic categories contain active or recurring shortages?
- How are shortages distributed across time?
- Are shortage records concentrated within specific molecular clusters?
- How do molecular properties differ across compounds and clusters?
- How do shortage events align with manufacturer market timelines?
- Which combinations of company, category, status, and molecular profile require further investigation?

## Solution

The project integrates multiple datasets into a Power BI analytical model.

### Data Domains

| Data Domain | Purpose |
|---|---|
| FDA drug shortage data | Analyze shortage status, manufacturer, therapeutic category, and posting dates |
| ChEMBL molecular data | Examine molecular weight, logP, hydrogen-bond acceptors, and hydrogen-bond donors |
| UMAP cluster output | Visualize chemically similar compounds in two dimensions |
| Cluster summary data | Compare average molecular properties across clusters |
| Manufacturer stock data | Review company market movement over time |
| Date dimension | Support consistent time-based filtering and analysis |

## Project Architecture

```text
FDA Drug Shortage Data ───────┐
                              │
ChEMBL Molecular Data ────────┤
                              │
UMAP Cluster Output ──────────┼── Power BI Data Model ── Interactive Dashboard
                              │
Cluster Summary Data ─────────┤
                              │
Manufacturer Stock Data ──────┤
                              │
Date Dimension ───────────────┘
```

## Data Model

The Power BI model uses a hybrid star and snowflake structure to connect datasets with different levels of granularity.

### Main Tables

#### `fda shortage`

Contains pharmaceutical shortage records, including fields related to:

- Drug or product name
- Manufacturer
- Therapeutic category
- Shortage status
- Initial posting date
- Discontinuation information

#### `cluster output`

Contains compound-level molecular information and UMAP coordinates, such as:

- Compound identifier
- Molecular weight
- logP
- Hydrogen-bond acceptors
- Hydrogen-bond donors
- UMAP X coordinate
- UMAP Y coordinate
- Cluster assignment
- Shortage indicator

#### `cluster summary`

Stores cluster-level aggregate statistics for comparing groups of chemically similar compounds.

Example measures include:

- Average molecular weight
- Average logP
- Average hydrogen-bond acceptors
- Average hydrogen-bond donors
- Compound count

#### `shortage match`

Acts as a bridge table between shortage records and molecular compound records when a direct one-to-one relationship is not available.

#### `stock data`

Contains time-series market information for pharmaceutical manufacturers or related companies.

#### `date table`

Provides a continuous calendar for:

- Year
- Quarter
- Month
- Week
- Day
- Time-based filtering
- Relationship management across event and market datasets

## Key Features

### Drug Shortage Analysis

- Explore shortage records by manufacturer
- Filter by therapeutic category
- Compare active and discontinued shortages
- Review shortage activity over time
- Investigate company-level concentration

### Chemical Cluster Explorer

- Visualize compounds using UMAP coordinates
- Explore groups of chemically similar compounds
- Compare shortage and non-shortage records
- Inspect molecular properties through interactive filtering
- Identify clusters that may require deeper analysis

### Molecular Profile Comparison

- Compare molecular weight across compounds and clusters
- Analyze logP distributions
- Review hydrogen-bond acceptor and donor patterns
- Examine whether shortage records are concentrated around specific chemical profiles

### Manufacturer and Market Context

- Align shortage events with stock timelines
- Compare manufacturers across selected periods
- Investigate whether market movement and shortage activity overlap
- Support further business and statistical analysis

### Interactive Power BI Filtering

Users can filter the dashboard by:

- Manufacturer
- Drug
- Therapeutic category
- Shortage status
- Chemical cluster
- Molecular property
- Date range
- Market ticker or company

## Key Design Decisions

### 1. Combining Multiple Data Domains

The project does not analyze shortage records in isolation. It connects regulatory, chemical, and financial information to provide a broader analytical view.

### 2. Using UMAP for Molecular Visualization

Molecular descriptor data is high-dimensional. UMAP coordinates were used to represent chemically similar compounds in a two-dimensional space that can be explored within Power BI.

### 3. Creating a Bridge Table

Drug shortage records and ChEMBL compounds do not always share a clean one-to-one key. A bridge table was used to manage the relationship between the two domains.

### 4. Separating Fact, Dimension, and Aggregate Tables

The model separates detailed records, dimensions, bridge relationships, and cluster summaries to support clearer filtering and reduce the risk of misleading totals.

### 5. Adding a Dedicated Date Dimension

A continuous date table was included to support consistent time intelligence across shortage events and financial data.

## Challenges

### Entity Matching

Drug names and manufacturer names may appear in different formats across datasets. Matching shortage records to molecular compounds requires normalization and careful validation.

### Different Levels of Granularity

A shortage event, a chemical compound, a molecular cluster, and a daily stock value represent different types of records. Incorrect relationships between them can create duplicated values or inaccurate totals.

### Many-to-Many Relationships

Some drugs may be linked to multiple records, formulations, or compounds. The bridge table helps manage these relationships, but the matching logic still requires validation.

### Missing and Inconsistent Data

Public pharmaceutical datasets may contain missing values, inconsistent names, incomplete dates, or changing shortage statuses.

### Interpretation

An observed relationship between a chemical cluster, manufacturer, stock movement, and shortage event does not prove causation. The dashboard is designed for exploration and investigation.

## Practical Value

The project provides a single analytical environment where users can:

- Review drug shortage records
- Compare manufacturers and therapeutic categories
- Explore molecular similarity
- Analyze chemical property patterns
- Examine shortage timelines
- Add market context
- Identify areas that require further statistical or operational investigation

The current version supports descriptive and exploratory analytics. It should not be presented as a validated prediction system.

## Technologies Used

- Microsoft Power BI
- Power Query
- DAX
- FDA drug shortage data
- ChEMBL molecular data
- UMAP cluster outputs
- Financial market data
- Data modeling
- Interactive data visualization

## Repository Structure

```text
Pharma_Risk_Analytics/
├── README.md
├── Riskmodel.pbix
├── Power_BI_Analytics.pdf
└── supporting project files
```

A future repository structure could include:

```text
Pharma_Risk_Analytics/
├── README.md
├── dashboard/
│   └── Riskmodel.pbix
├── reports/
│   └── Power_BI_Analytics.pdf
├── images/
│   ├── dashboard-overview.png
│   ├── data-model.png
│   ├── cluster-explorer.png
│   └── shortage-timeline.png
├── data/
│   └── README.md
├── dax/
│   └── measures.md
├── docs/
│   ├── data-dictionary.md
│   ├── methodology.md
│   └── limitations.md
└── LICENSE
```

## How to Use the Project

1. Clone or download the repository.

```bash
git clone https://github.com/lakshman199/Pharma_Risk_Analytics.git
```

2. Open `Riskmodel.pbix` using Microsoft Power BI Desktop.

3. Review the data-source settings and update local file paths if required.

4. Refresh the dataset.

5. Use the dashboard filters to explore shortage records, manufacturers, chemical clusters, molecular properties, and time periods.

## Recommended Dashboard Pages

### Executive Overview

A high-level view of:

- Total shortage records
- Active shortages
- Discontinued shortages
- Manufacturer distribution
- Therapeutic category distribution
- Shortage activity over time

### Chemical Cluster Explorer

A UMAP scatter plot showing:

- UMAP X and Y coordinates
- Compound-level records
- Cluster assignments
- Shortage indicators
- Molecular-property tooltips

### Molecular Profile Analysis

Comparisons of:

- Molecular weight
- logP
- Hydrogen-bond acceptors
- Hydrogen-bond donors
- Cluster-level averages

### Shortage Timeline

Time-based analysis of:

- Initial posting dates
- Current and discontinued status
- Manufacturer trends
- Therapeutic category trends

### Market Context

A comparison of:

- Manufacturer stock trends
- Shortage event dates
- Selected companies
- Time periods

## Limitations

- The project is intended for exploratory analysis.
- Observed relationships do not establish causation.
- Drug-to-compound matching quality affects downstream results.
- Chemical similarity does not necessarily imply manufacturing similarity.
- Stock-price movement may be affected by many external factors.
- The current repository does not document a fully automated data-refresh pipeline.
- Statistical significance testing is not included in the current version.
- No validated forecasting or classification model is included.
- The dashboard should not be used for clinical decisions or investment advice.

## Future Improvements

- Build a reproducible ETL pipeline
- Automate data collection and refresh
- Add drug-name and manufacturer entity-resolution rules
- Introduce data-quality validation checks
- Document Power Query transformations
- Document DAX measures
- Add a detailed data dictionary
- Measure shortage duration
- Analyze manufacturer concentration
- Perform statistical hypothesis testing
- Validate relationships between molecular clusters and shortages
- Build an explainable shortage-risk model
- Compare classification and forecasting approaches
- Add Power BI Service deployment
- Configure scheduled refresh
- Add dashboard screenshots and architecture diagrams

## Resume Summary

Built a Power BI pharmaceutical risk analytics dashboard for supply-chain and regulatory analysis using FDA shortage records, ChEMBL molecular descriptors, UMAP clusters, and manufacturer stock data to explore shortage patterns across drugs, companies, chemical profiles, and time.

## Disclaimer

This project is intended for educational, portfolio, and exploratory analytical purposes.

It does not provide medical advice, regulatory guidance, investment advice, or a validated forecast of future pharmaceutical shortages.

## Author

**Lakshman Ega**

- GitHub: [lakshman199](https://github.com/lakshman199)
