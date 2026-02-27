# Methodology: Project 2 — Cartographic Modelling of Old Growth Forests on Vancouver Island

This document contains the detailed step-by-step methodology followed in Project 2.

---

## Task 1: Query and Export Data from UBC PostgreSQL Server
- Connected to the UBC PostgreSQL server from ArcGIS Pro using a new database connection
- Wrote a SQL query to select managed forest polygons from the VRI table, returning only the fields needed for analysis (`gid`, `bec_zone_code`, `bec_subzone`, `proj_age_1`, `geom`)
- Exported the query result as a local geodatabase feature class named `forest_land_base`
- Exported `vancouver_island_own`, `vancouver_island_human_disturbance`, and `vancouver_island_landscape_units` directly to the local project geodatabase
- Selected crown land polygons from `vancouver_island_own` using a `LIKE 'Crown%'` SQL pattern and exported as `crown_land`
- Used the Pairwise Intersect tool to identify the overlap between `forest_land_base` and `crown_land`, producing `Crown_Forest`
- Visualized the `Crown_Forest` layer symbolized by BEC zone and subzone

---

## Task 2: Classify Seral Stages
- Added a new text field called `Seral_Stage` to the `Crown_Forest` attribute table
- Used the ArcGIS Field Calculator with a Python code block to classify each polygon into Early, Mid, Mature, or Old seral stage based on BEC zone and estimated stand age (`proj_age_1`)
- Age thresholds varied by BEC zone (CWH, MH, CDF) to reflect differences in forest productivity
- Selected polygons that intersect with current human disturbance areas (`cef_human_disturb_flag = 'Human Disturb Current 20yr'`) and reclassified their `Seral_Stage` to Early
- Used Pairwise Intersect to divide `Crown_Forest` by `vancouver_island_landscape_units`, producing `CrownForest_LU`

---

## Task 3: Calculate Percentage of Old Growth Forests
- Added a new text field `LU_BEC` to `CrownForest_LU` combining Landscape Unit ID, BEC zone, and BEC subzone as a unique identifier
- Used the Dissolve tool on `CrownForest_LU` by `LU_BEC` to calculate total crown forest area per unit, producing `Total_Forest_Area`
- Selected only Old seral stage polygons and dissolved again to produce `Old_Forest_Area`
- Joined `Old_Forest_Area` back to `Total_Forest_Area` using Join Field on `LU_BEC`
- Added a `PercentOld` (Double) field and calculated old growth percentage using a Python expression
- Added a `DiffFromHigh` (Double) field and wrote a custom Python expression to calculate the difference between the calculated old growth percentage and the BEC subzone-specific provincial high threshold
- Applied graduated colour symbology to `DiffFromHigh` to visualize where units exceed, meet, or fall below provincial targets
- Produced a final map layout in ArcGIS Pro including title, legend, north arrow, scale bar, and author information
- Exported the final map layout as a PNG file

---

*Back to [README](README_project2.md)*
