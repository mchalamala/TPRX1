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
│── deseq2/              # Differential expression analysis 
│── filtering/           # Filtering significant differentially expressed genes
│── heatmap/             # Heatmap visualization of totipotency markers
│── scoring_algorithm.py # Totipotency scoring algorithm
│── volcanoplot/         # Volcano plot generation for DE results
```

---

## **Datasets Used**
The following datasets were analyzed to identify totipotency markers and evaluate totipotent-like transcriptional signatures:

### **RNA-seq, Ribo-seq, and STACC-seq Data**
- Translatome and transcriptome co-profiling reveals a role of TPRXs in human zygotic genome activation (Zou et al.)

### **8CLC Datasets for Totipotency Scoring**
- 8C-like cells capture the human zygotic genome activation program in vitro (Taubenschmid-Stowers et al., 2022)
- Recapitulating early human development with 8C-like cells (Yu et al., 2022)
- Revealing cell populations catching the early stages of human embryo development in naive pluripotent stem cell cultures (Moya-Jódar et al., 2023)
- Transient DUX4 expression in human embryonic stem cells induces blastomere-like expression program that is marked by SLC34A2 (Yoshihara et al., 2022)
- Single-cell RNA-Seq profiling of human preimplantation embryos and embryonic stem cells (Yan et al., 2013)

---

## **Analysis Pipeline**
### **1. Differential Expression Analysis (`deseq2`)**
- Uses DESeq2 to identify differentially expressed genes (DEGs) from Zou et al.
- Processes count data to compute log2FoldChange and adjusted p-values (`padj`)
- Outputs: `deseq2_results.csv`

### **2. Gene Filtering (`filtering`)**
- Filters significantly upregulated and downregulated genes based on:
  - `padj < 0.05`
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
[1] rargelaguet, “GitHub - rargelaguet/DUX4_8CLC_hESCs: DUX4_ hESCs_multiome,” GitHub, 2021. https://github.com/rargelaguet/DUX4_8CLC_hESCs (accessed Feb. 17, 2025).
‌[2] ChenManqi2, “GitHub - ChenManqi2/ci8CLC_scripts,” GitHub, 2022. https://github.com/ChenManqi2/ci8CLC_scripts (accessed Feb. 17, 2025).
‌[3] my0916, “GitHub - my0916/STRT2: STRT2-NextSeq analysis pipeline,” GitHub, 2019. https://github.com/my0916/STRT2 (accessed Feb. 17, 2025).
‌[4] Z. Zou et al., “Translatome and transcriptome co-profiling reveals a role of TPRXs in human zygotic genome activation,” Science (New York, N.Y.), vol. 378, no. 6615, p. abo7923, Oct. 2022, doi: https://doi.org/10.1126/science.abo7923.
[5] L. Delisle, M. Doyle, and F. Heyl, “Hands-on: Hands-on: ATAC-Seq data analysis,” Galaxy Training Network, Nov. 03, 2023. https://training.galaxyproject.org/training-material/topics/epigenetics/tutorials/atac-seq/tutorial.html
