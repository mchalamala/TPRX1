# **TPRX1 Totipotency Analysis**

## **Overview**
This repository contains scripts for analyzing TPRX1-associated totipotency signatures using publicly available RNA-seq, Ribo-seq, and STACC-seq datasets from Zou et al. Additionally, it evaluates totipotency markers across multiple datasets, with Yan et al. (2013) as a reference for totipotency scoring.

The analysis pipeline includes:
- Differential expression analysis (DESeq2)
- Gene filtering
- Heatmap visualization
- Volcano plot generation
- Totipotency scoring of 8CLC clusters

---

## Repository Structure
```
TPRX1/
│── deseq2/              # Differential expression analysis (Zou et al.)
│── filtering/           # Filtering significant differentially expressed genes
│── heatmap/             # Heatmap visualization of totipotency markers
│── scoring_algorithm.py # Totipotency scoring algorithm
│── volcanoplot/         # Volcano plot generation for DE results
```

---

## **Datasets Used**
The following datasets were analyzed to identify totipotency markers and evaluate totipotent-like transcriptional signatures:

### **RNA-seq, Ribo-seq, and STACC-seq Data**
- Zou et al. (Publicly available RNA-seq, Ribo-seq, and STACC-seq datasets)

### **8CLC Datasets for Totipotency Scoring**
- Taubenschmid-Stowers et al., 2022
- Yu et al., 2022
- Moya-Jódar et al., 2023
- Yoshihara et al., 2022
- Yan et al., 2013

---

## **Analysis Pipeline**
### **1. Differential Expression Analysis (`deseq2`)**
- Uses DESeq2 to identify differentially expressed genes (DEGs) from Zou et al.
- Processes count data to compute log2FoldChange and adjusted p-values (`padj`)
- Outputs: `deseq2_results.csv`

### **2. Gene Filtering (`filtering`)**
- Filters significantly upregulated and downregulated genes based on:
  - `padj < 0.06`
  - `log2FoldChange > 2` (upregulated) or `< -2` (downregulated)
- Outputs: `filtered_genes.xlsx`

### **3. Heatmap Generation (`heatmap`)**
- Generates heatmaps of totipotency marker expression
- Outputs: `heatmap.png`

### **4. Volcano Plot (`volcanoplot`)**
- Plots log2FoldChange vs -log10(padj) for visualization
- Highlights significantly up/down-regulated genes
- Outputs: `volcano_plot.png`

### **5. Totipotency Scoring (`scoring_algorithm.py`)**
- Identifies most totipotent cell clusters based on marker expression
- Uses Yan et al. (2013) as the reference dataset (100% normalization score)
- Outputs:
  - `totipotency_scores.csv` – Totipotency scores for all cells
  - `totipotency_scores_8CLC.csv` – Scores for **8CLC clusters only**

---

## **Totipotency Scoring Interpretation**
The analysis produces two key scoring metrics:
1. Normalized Totipotency Score:
   - Measures the proportion of totipotent-like cells in each dataset
   - Yan et al. (2013) is set to 100% (reference)
   - Example: Yoshihara et al. (2022) had the highest normalized score (0.83%), indicating more totipotent cells than other datasets

2. 8CLC Clustered Totipotency Score:
   - Actual measure of totipotency potential
   - Computed from cells assigned to the 8CLC cluster
   - Example: Yoshihara et al. (2022) had the highest clustered score (721.4691), confirming its robust totipotency signature

---

## **Dependencies**
### **R Packages**
```r
install.packages(c("Seurat", "ggplot2", "dplyr", "readxl", "Matrix", "hdf5r"))
BiocManager::install("DESeq2")
```
### **Python Packages**
```python
pip install pandas openpyxl matplotlib seaborn
```

---

## **Running the Analysis**
1. Run `deseq2` for differential expression analysis (Zou et al. datasets)
2. Filter significant genes using `filtering`
3. Generate heatmaps using `heatmap`
4. Visualize differential expression using `volcanoplot`
5. Compute **totipotency scores** using `scoring_algorithm.py`

---

## **Outputs**
- `deseq2_results.csv` – DESeq2 results from Zou et al.
- `filtered_genes.xlsx` – List of significant genes
- `heatmap.png` – Heatmap of totipotency marker expression
- `volcano_plot.png` – Volcano plot highlighting DEGs
- `totipotency_scores.csv` – Totipotency scores across all datasets
- `totipotency_scores_8CLC.csv` – 8CLC-specific totipotency scores

---

## **Citations**
I do this later
