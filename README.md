# 01_mk_data_rubric_clean

**Author:** Derik Suria  
**Last Updated:** 5/28/2025  
**Purpose:** This project processes and summarizes survey response data from Qualtrics to support analysis of data use practices across organizations.  
🛠️ **IMPORTANT**: All file paths that save outputs (e.g., `.csv`, `.pdf`) are hardcoded by default. Update file destinations based on your system.


---

## What This Script Does

This R Markdown script performs the following:

1. **Connects to the Qualtrics API**  
   - Uses your personal API key and data center to fetch raw survey responses.

2. **Loads Mapping Data**  
   - Reads a crosswalk file (`pillar_question_xw.xlsx`) that maps survey questions to categories ("pillars").

3. **Cleans & Recodes Data**  
   - Recodes raw survey responses (e.g., `1`, `2`, `3`, `4`) into descriptive categories ("Emerging", "Developing", etc.).
   - Standardizes organization names.

4. **Generates Summary Tables**  
   - At the **pillar** level (themes),
   - At the **construct** level (sub-themes),
   - And at the **indicator** level (individual questions).

5. **Exports Data**  
   - Saves clean summary tables to CSV files.
   - Creates one summary CSV per organization for both pillar and indicator data.
   - **🛠️ Tip:** All file paths used for saving data (e.g., `output/summary_tables/`) can be edited.

---

## Input Files

| File | Description |
|------|-------------|
| `pillar_question_xw.xlsx` | Excel crosswalk that maps questions to pillars and indicators. |

---

## Output Files

| File | Location |
|------|----------|
| `org_pillar_clean.csv` | `output/summary_tables/` |
| `org_indicator_clean.csv` | `output/summary_tables/` |
| `<org>.csv` | `output/pillar_tables/!overall/` |
| `<pillar>.csv` | `output/pillar_tables/<org>/` |

---

## Required R Packages

Make sure the following packages are installed:

```r
install.packages(c("tidyverse", "patchwork", "qualtRics"))
```

# 02_gen_bar_charts

**Author:** Derik Suria  
**Last Updated:** 5/28/2025  
**Purpose:** This script automates the creation of stacked bar charts summarizing survey responses, grouped by **pillar** and **construct**, for each organization.

---

## What This Script Does

### 🔹 Chart Type 1: Responses by Pillar (All Organizations)
- Groups survey responses by **pillar** (e.g., Strategic Data Leadership).
- Calculates the **percentage** of each response type.
- Visualizes this in a **stacked bar chart** for all organizations.

### 🔹 Chart Type 2: Responses by Pillar (Per Organization)
- Groups survey responses by **pillar** (e.g., Strategic Data Leadership).
- Calculates the **percentage** of each response type.
- Visualizes this in a **stacked bar chart** per organization.

### 🔹 Chart Type 3: Responses by Construct (Per Organization)
- Further drills down to **constructs** (subsections under each pillar).
- Builds 5 stacked bar charts per construct for each organization.

All chart types are saved as PDF files.

---

## Inputs

- `org_pillar_clean.csv`  
  → Cleaned summary data at the pillar level.
- `org_indicator_clean.csv`  
  → Cleaned summary data at the construct (indicator) level.

These should exist in the following directory: /output/summary_tables/

---

## Output

Charts are saved as PDF files in:

| Output Directory | File Description |
|------------------|------------------|
| `/output/summary_charts/`     | One PDF including all organizations showing pillar-level results (like slide 7) |
| `/output/pillar_charts/overall`     | Five PDFs per organization showing pillar-level results (like slide 8) |
| `/output/pillar_charts/`     | One PDF per organization showing pillar-level results |

---

## Required R Packages

Ensure the following libraries are installed:

```r
install.packages(c("tidyverse", "patchwork"))
library(tidyverse)
library(patchwork)

