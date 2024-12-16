# **Enrichment Analysis in R for Liver Cancer Data**

## **Project Overview**

This repository contains data, scripts, and results for enrichment analysis on gene expression datasets related to colorectal cancer and hepatocellular carcinoma (HCC). The goal is to identify differentially expressed genes (DEGs) and perform enrichment analysis to uncover pathways and biological processes associated with specific conditions like relapse, recurrence, and vascular invasion.

---

## **Highlights**

- **Packages Used**:  
  - `tidyverse` – Data manipulation and visualization  
  - `dplyr` – Data filtering and wrangling  
  - `enrichR` – Enrichment analysis  
  - `openxlsx` – Excel file generation  
  - `ggplot2` – Data visualization  
  - `knitr` – Reproducible report generation  

- **Code**:  
  R Markdown scripts and custom functions for performing differential expression analysis, enrichment analysis, and generating outputs.

- **Reproduced Outputs**:  
  - T-test results for DEGs  
  - Enrichment analysis results in Excel and TSV formats  
  - Compiled PDF and HTML reports  
  - Circos plots and pathway visualizations  

---

## **Repository Organization**

```
Enrichment_Analysis/
│
├── input/                           # Raw and processed input data
│   ├── 2023-EnrichR-Databases.txt
│   ├── CRC_PILOT_clinical_data_HIDS.tsv
│   ├── CRC_PILOT_withGeneAnno.tsv
│   ├── CRCPilot_GeneExp_Relapse_(Comp).vs._RelapseFree_(Base).TTest.csv
│   └── CRCPilot_Ttest_Shortlisted.csv
│
├── scripts/                         # R Markdown scripts and custom functions
│   ├── Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd
│   ├── Aizhan-Uteubayeva-EnrichR.Rmd
│   ├── 04-EnrichR.Rmd
│   ├── functionEnrichment.R
│   └── Week7_Enrich.Rproj
│
├── output/                          # Output files and analysis results
│   ├── ColonCancer_EnrichR.xlsx
│   ├── shortListedUniqueGenes.tsv
│   ├── TTest_results_shortlist2.csv
│   ├── Aizhan_Uteubayeva_TopFeatures.tsv
│   ├── Aizhan_Uteubayeva-TTestHW-06-Output.csv
│   └── Aizhan_Uteubayeva_Circos.pdf.pdf
│
├── reports/                         # Compiled reports
│   ├── Aizhan_Uteubayeva_EnrichR.pdf
│   └── 04-EnrichR.pdf
│
└── README.md                        # Project documentation
```

---

## **Methodology**

### **1. Data Preparation**

#### **Input Files**

1. **Clinical and Gene Expression Data**:  
   - `CRC_PILOT_clinical_data_HIDS.tsv`: Clinical data for colorectal cancer patients.  
   - `CRC_PILOT_withGeneAnno.tsv`: Log2-normalized gene expression data with annotations.  

2. **T-Test Results**:  
   - `CRCPilot_GeneExp_Relapse_(Comp).vs._RelapseFree_(Base).TTest.csv`: T-test results comparing relapse and relapse-free groups.  
   - `CRCPilot_Ttest_Shortlisted.csv`: Filtered significant genes from T-test results.  

3. **EnrichR Databases**:  
   - `2023-EnrichR-Databases.txt`: List of EnrichR databases for enrichment analysis.

#### **Scripts**

- **Differential Gene Expression Analysis**:  
  - `Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd`: Performs T-tests to identify DEGs.

- **Enrichment Analysis**:  
  - `Aizhan-Uteubayeva-EnrichR.Rmd` and `04-EnrichR.Rmd`: Scripts for enrichment analysis using EnrichR.  
  - `functionEnrichment.R`: Custom function for batch enrichment analysis.

---

### **2. Differential Gene Expression Analysis**

1. **Read and Clean Data**:  
   ```r
   clinData <- read.table("input/CRC_PILOT_clinical_data_HIDS.tsv", sep="\t", header=TRUE)
   geneExp <- read.table("input/CRC_PILOT_withGeneAnno.tsv", sep="\t", header=TRUE, row.names=1)
   ```

2. **Filter and Subset Data**:  
   ```r
   geneExpFiltered <- geneExp %>% select(-contains("Normal"))
   ```

3. **Perform T-Tests**:  
   ```r
   source("scripts/Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd")
   ```

4. **Output**:  
   - `output/Aizhan-Uteubayeva-TTestHW-06-Output.csv`: Full T-test results.  
   - `output/Aizhan_Uteubayeva_TopFeatures.tsv`: Top DEGs.

---

### **3. Enrichment Analysis**

1. **Prepare Gene List**:  
   ```r
   shortlistedGenes <- read.csv("input/CRCPilot_Ttest_Shortlisted.csv")$Gene
   ```

2. **Load EnrichR Databases**:  
   ```r
   dbList <- readLines("input/2023-EnrichR-Databases.txt")
   ```

3. **Run Batch Enrichment**:  
   ```r
   source("scripts/functionEnrichment.R")
   functionEnrichment(dbList, shortlistedGenes, "output/ColonCancer_EnrichR.xlsx")
   ```

4. **Output**:  
   - `output/ColonCancer_EnrichR.xlsx`: Enrichment results.  
   - `output/shortListedUniqueGenes.tsv`: Final shortlisted genes.

---

## **Steps to Reproduce the Analysis**

1. **Set Up Environment**:  
   Install required R packages:  
   ```r
   install.packages(c("tidyverse", "enrichR", "openxlsx", "dplyr", "knitr", "ggplot2"))
   ```

2. **Clone the Repository**:  
   ```bash
   git clone https://github.com/yourusername/Enrichment_Analysis.git
   cd Enrichment_Analysis
   ```

3. **Prepare Data**:  
   Ensure all input files are placed in the `input/` directory.

4. **Run Scripts**:  
   - **Differential Expression Analysis**:  
     ```r
     rmarkdown::render("scripts/Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd")
     ```
   - **Enrichment Analysis**:  
     ```r
     rmarkdown::render("scripts/04-EnrichR.Rmd")
     ```

5. **View Results**:  
   - T-test results in `output/Aizhan-Uteubayeva-TTestHW-06-Output.csv`  
   - Enrichment results in `output/ColonCancer_EnrichR.xlsx`  
   - Compiled reports in `reports/`

---

## **Skills Demonstrated**

- **Bioinformatics Analysis**: Differential expression and enrichment analysis.  
- **Data Cleaning and Transformation**: Filtering clinical and gene expression data.  
- **Reproducible Research**: R Markdown and custom functions.  
- **Data Visualization**: Generating circos plots and enrichment results.  
- **Automation**: Batch enrichment analysis using EnrichR.

---

## **Author**

**Aizhan Uteubayeva**

---

## **License**

This project is licensed under the **MIT License**. See the `LICENSE` file for details.
