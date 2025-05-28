# sdp-data-use-rubric
# mk_data_rubric_clean

**Author:** Derik Suria  
**Last Updated:** `r format(Sys.time(), '%B %d, %Y')`  
**Purpose:** This project processes and summarizes survey response data from Qualtrics to support analysis of data use practices across organizations.

---

## 🚀 What This Script Does

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

---

## 📂 Input Files

| File | Description |
|------|-------------|
| `qualtrics_download_may_7.csv` | Raw Qualtrics survey export (if not using API). |
| `pillar_question_xw.xlsx` | Excel crosswalk that maps questions to pillars and indicators. |

---

## 📤 Output Files

| File | Location |
|------|----------|
| `org_pillar_clean.csv` | `output/summary_tables/` |
| `org_indicator_clean.csv` | `output/summary_tables/` |
| `pillar_<org>.csv` | `output/pillar_tables/` |
| `indicator_<org>.csv` | `output/indicator_tables/` |

---

## 📦 Required R Packages

Make sure the following packages are installed:

```r
install.packages(c("tidyverse", "patchwork", "qualtRics"))
