# RNA-seq Differential Expression Pipeline

## Problem
This project implements a complete, end-to-end bioinformatics workflow to process raw RNA-seq reads, quantify gene expression, identify differentially expressed (DE) genes, and perform functional enrichment analysis to interpret biological significance.

## Methods
The pipeline is structured into two main phases: read processing (Galaxy) and statistical analysis (R/Bioconductor).

*   **Read Processing and Quantification (Galaxy Pipeline):**
    *   **Quality Control:** **FastQC** is used to assess the quality of raw sequence reads.
    *   **Trimming:** **Cutadapt** is employed to remove adapter sequences and low-quality bases.
    *   **Alignment:** Reads are aligned to a reference genome using **HISAT2**, a splice-aware aligner.
    *   **Quantification:** **featureCounts** is used to count the number of reads mapping to each gene feature, generating a raw count matrix.
*   **Differential Expression Analysis (R/Bioconductor):**
    *   The raw count matrix is loaded into R.
    *   Lowly expressed genes are filtered out.
    *   Normalization is performed using either the **limma-voom** (TMM normalization) or **DESeq2** (median-of-ratios) method.
    *   Statistical modeling is applied to identify significantly differentially expressed genes (FDR < 0.05).
*   **Post-DE Analysis:**
    *   **Visualisation:** Scripts generate essential plots, including **Principal Component Analysis (PCA)** for quality assessment, **Volcano Plots** (significance vs. fold-change), and **MA Plots** (mean-average).
    *   **Enrichment:** Functional analysis is performed using **clusterProfiler** to determine enriched Gene Ontology (GO) terms and KEGG pathways.

## Results
The pipeline produces high-quality, reproducible output for both technical quality control and biological insight.

*   Output table: `results/tables/de_results_fdr0.05.csv` (contains log2FC, p-value, and FDR for all DE genes)
*   Figure(s): `results/figures/pca_plot.png`, `results/figures/volcano_plot.png`, `results/figures/ma_plot.png`, `results/figures/go_enrichment_plot.png`

## Reproducibility
* The analysis environment is managed using `conda` to ensure all package versions are consistent.
  ```bash
  conda env create -f environment.yml
  conda activate rnaseq-de-env
  python scripts/run_pipeline.py --input data/raw_reads/ --sample-sheet config/samples.tsv



## Skills Demonstrated
*  RNA-seq Data Handling: 
    Proficiency in quality control, trimming, alignment, and quantification using industry-standard      tools (FastQC, Cutadapt, HISAT2, featureCounts, MultiQC).
*  Bioconductor Statistical Analysis:
    Expertise in applying advanced statistical methods for differential expression using limma-voom      and/or DESeq2 package workflows.
*  Data Visualisation & Interpretation:
    Ability to generate and interpret key bioinformatics plots (PCA, Volcano, MA plots) for
    assessing data quality and presenting results.
*  Functional Genomics:
    Application of the clusterProfiler package to perform Gene Ontology and KEGG pathway enrichment       analysis, linking DE genes to biological function.
*  Reproducible Coding Practices:
    Creation of a version-controlled, modular workflow using a command-line interface and package        management (conda/environment.yml).
   
## Next Improvements
*  Limitation / Planned Improvement: 
    *  Integrate Rmarkdown notebooks for interactive, narrative-driven    presentation of the
       results and code, moving beyond static R scripts.
    *  Implement a pipeline management system (e.g., Snakemake or Nextflow) to manage dependencies,
       parallelize tasks, and ensure robust re-runability of the entire workflow.

