# Cartographic Modelling of Old Growth Forests on Vancouver Island

## Overview
This project analyses the distribution of old growth forests across Vancouver Island, British Columbia, using forest inventory data and the BC Cumulative Effects Framework (CEF). The analysis identifies crown forest land, classifies stands by seral stage, and compares calculated old growth percentages against provincial targets by Landscape Unit and BEC subzone. Results are visualized as a cartographic map showing where forests fall short of, meet, or exceed old growth targets.

---

## Objectives
- Query and extract forest inventory data from a remote PostgreSQL server
- Prepare and clean spatial layers for old growth analysis
- Classify forest stands by seral stage using BEC zone age thresholds
- Calculate old growth area and percentage by Landscape Unit and BEC subzone
- Compare results against provincial old growth targets
- Produce a map communicating old growth distribution across Vancouver Island

---

## Data Sources & Tools

**Data**

| Layer | Description | Source |
|-------|-------------|--------|
| `vancouver_island_vri` | Vegetation Resource Inventory 2024 | [BC Data Catalogue](https://catalogue.data.gov.bc.ca/dataset/vri-2024-forest-vegetation-composite-layer-1-l1-) |
| `vancouver_island_own` | Generalized Forest Cover Ownership | [BC Data Catalogue](https://catalogue.data.gov.bc.ca/dataset/generalized-forest-cover-ownership) |
| `vancouver_island_human_disturbance` | CEF Human Disturbance (current) | [BC Data Catalogue](https://catalogue.data.gov.bc.ca/dataset/bc-cumulative-effects-framework-human-disturbance-current) |
| `vancouver_island_landscape_units` | Landscape Units of BC (current) | [BC Data Catalogue](https://catalogue.data.gov.bc.ca/dataset/landscape-units-of-british-columbia-current) |

All layers were accessed via the UBC PostgreSQL Server (`FRST-PostgreSQL.ead.ubc.ca`).

**Tools**

| Tool | Purpose |
|------|---------|
| ArcGIS Pro | Spatial analysis, field calculations, and map production |
| PostgreSQL / SQL | Querying and extracting data from the remote server |
| Python (ArcGIS Field Calculator) | Classifying seral stages and calculating old growth targets |

---

## Methods
Forest inventory data was queried from the UBC PostgreSQL server and filtered to managed crown forests on Vancouver Island. Stands were classified into seral stages (Early, Mid, Mature, Old) using BEC zone-specific age thresholds. Human-disturbed areas were identified and reclassified as Early seral. Old growth area and total forest area were summarized by Landscape Unit and BEC subzone combination, and the percentage of old growth was calculated. A difference field was computed to show how each unit compares to the provincial high old growth threshold, and results were visualized as a graduated colour map.

📄 *For a detailed breakdown of the methodology, [click here](https://github.com/AgnessChisale/cartographic_modelling_of_old_growth/blob/main/methodology_project2.md)*

---

## Outputs

- `map_diff_from_high_threshold.png` — Map showing the difference between calculated old growth percentage and provincial high targets, by Landscape Unit and BEC subzone
- Summary table with fields for Total Area, Old Growth Area, and Percentage Old Growth

---

## Key Findings
- Old growth forest distribution varies significantly across Landscape Units and BEC subzones on Vancouver Island
- Many units fall below the provincial high old growth threshold, particularly in heavily disturbed areas
- The CEF framework reveals spatial patterns of old growth deficit that reflect historical logging pressure

---

## Skills Learned
- Querying a remote PostgreSQL database from ArcGIS Pro using SQL
- Filtering and exporting spatial layers using Select by Attributes and Pairwise Intersect
- Writing Python expressions in the ArcGIS Field Calculator
- Classifying forest stands by seral stage using BEC zone age thresholds
- Dissolving polygons and summarizing area statistics
- Joining attribute tables using Join Field
- Calculating percentage fields and difference metrics
- Producing a professional map layout in ArcGIS Pro
