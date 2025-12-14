# RNA-seq mini-project — Salmon → DESeq2 (Mouse, mm10)

This repository contains a reproducible RNA-seq differential expression pipeline
based on Salmon, tximport, and DESeq2, applied to a mouse dataset (mm10, GENCODE).

The goal of this mini-project was to practice RNA-seq data analysis concepts **in parallel with the Bioinformatics Methods for Transcriptomics course**
(Johns Hopkins University, Coursera), with a focus on:
- transcript-level quantification with Salmon
- gene-level summarization with tximport
- differential expression analysis with DESeq2
- writing a fully reproducible R script (no interactive-only analysis)

---

## Data source and timeline

- Dataset: GSE83931 (mouse RNA-seq)
- Source: Dataset used in the course
  Bioinformatics Methods for Transcriptomics  
  Johns Hopkins University — Coursera
- Organism: Mouse (mm10)
- Project duration: December 6–14, 2025

This project was conducted **alongside the course**, with the objective of implementing a complete RNA-seq workflow under **realistic local computing constraints**.

Due to **hardware and memory limitations on a personal laptop**, some tools presented in the course (e.g. STAR and other memory-intensive aligners) could not be run locally.
To address this, the analysis was performed under **Linux using Windows Subsystem for Linux (WSL)**, and a lightweight, transcript-level quantification approach (**Salmon**) was chosen as a technically appropriate and resource-efficient alternative.

---

## Project structure

    GSE83931_miniFASTQ/
    ├── data/
    │   └── metadata/
    │       └── samples.csv
    ├── reference/
    │   └── gencode_mm10/
    │       ├── gencode.vM23.transcripts.fa.gz
    │       └── tx2gene_from_fasta.tsv
    ├── results/
    │   ├── salmon/
    │   └── DESeq2/
    │       ├── DESeq2_results.csv
    │       ├── DESeq2_results_clean.csv
    │       ├── DESeq2_significant_padj0.1.csv
    │       ├── dds.rds
    │       ├── txi.rds
    │       ├── sessionInfo.txt
    │       └── run_log.txt
    ├── figures/
    │   ├── PCA_plot.pdf
    │   ├── MA_plot.pdf
    │   └── Volcano_plot.pdf
    └── scripts/
        └── RNAseq_Salmon_tximport_DESeq2.R

---

## Experimental design

- Organism: Mouse (mm10)
- Quantification: Salmon
- Annotation: GENCODE vM23
- Conditions:
  - CTRL (control)
  - TREAT (treated)
- Contrast tested: TREAT vs CTRL

---

## How to run the analysis

Run the pipeline from the project root:

    cd ~/projects/GSE83931_miniFASTQ
    Rscript scripts/RNAseq_Salmon_tximport_DESeq2.R

For maximum stability (recommended on laptops / WSL):

    nohup Rscript scripts/RNAseq_Salmon_tximport_DESeq2.R > results/DESeq2/nohup.out 2>&1 &

---

## Main outputs

- Differential expression (clean)  
  results/DESeq2/DESeq2_results_clean.csv

- Significant genes (padj < 0.1)  
  results/DESeq2/DESeq2_significant_padj0.1.csv

- Saved R objects  
  - dds.rds  
  - txi.rds

- Figures  
  - PCA plot  
  - MA plot  
  - Volcano plot

- Reproducibility  
  - sessionInfo.txt (R and package versions)  
  - run_log.txt (full execution log)

---

## Notes on reproducibility

- The pipeline rebuilds tx2gene automatically from the GENCODE FASTA if missing.
- Transcript identifiers are kept consistent with the Salmon index (GENCODE-style IDs).
- All steps are fully scripted; no results depend on interactive R history.

---

## Purpose of this project

This mini-project is part of a broader roadmap to:
- strengthen practical RNA-seq analysis skills
- build a portfolio of reproducible bioinformatics workflows
- prepare for advanced training and research in genomics and epigenetics
