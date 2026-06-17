# RNA-seq Pipeline for Biomarker Detection in Lung Adenocarcinoma (LUAD)

Reproducible bioinformatics pipeline for differential gene expression analysis and biomarker identification in lung adenocarcinoma, developed in R/RStudio.

---

## Dataset

| Field | Value |
|---|---|
| Source | Gene Expression Omnibus (GEO) |
| Accession | PRJNA320473 / SRP074349 |
| Samples | 20 (10 tumor + 10 normal, paired design) |
| Platform | Illumina HiSeq 2500, paired-end |
| Reference genome | GRCh38.p14 |
| Annotation | GENCODE v47 |

---

## Pipeline Structure

| Script | Description |
|---|---|
| `00_initial_setup.Rmd` | Environment verification, metadata consolidation, reference file checks |
| `01_quality_control.Rmd` | Quality control with FastQC and MultiQC |
| `02_genome_index_alignment.Rmd` | Genome index construction and read alignment with Rsubread |
| `03_quantification_featureCounts.Rmd` | Gene-level read quantification with featureCounts |
| `04_differential_expression_DESeq2.Rmd` | Differential expression analysis with DESeq2; PCA, volcano, MA, and heatmap |
| `05_functional_analysis.Rmd` | GO (BP/MF/CC), KEGG enrichment, and GSEA with clusterProfiler |
| `06_gene_symbol_mapping.Rmd` | ENSEMBL-to-symbol mapping; supplementary table generation |
| `07_WGCNA.Rmd` | Weighted gene co-expression network analysis; hub gene identification; PPI input |
| `08_figure_export.Rmd` | Publication-ready figure export at 300 dpi |

---

## Key Results

- **6,989 DEGs** identified (padj < 0.05, |log2FC| > 1)
  - 4,328 upregulated in tumor
  - 2,661 downregulated in tumor
- **log2FC range:** −7.40 to 22.79
- **GO terms enriched:** 1,384
- **KEGG pathways enriched:** 38
- **GSEA:** 585 GO terms, 50 KEGG pathways
- **Top upregulated genes:** CSN1S1, PADI3, MMP13, COL11A1
- **Top downregulated genes:** SLC6A4, ITLN1, CA4
- **WGCNA:** 3 tumor-associated modules (blue, turquoise, brown); 19 consensus hub genes via PPI + cytoHubba (MCC, MNC, EPC, Degree)

---

## Requirements

### Software

| Tool | Version |
|---|---|
| R | 4.4.2 |
| RStudio | — |
| FastQC | 0.12.1 |
| MultiQC | 1.27 |

### R / Bioconductor Packages

| Package | Version |
|---|---|
| Rsubread | 2.20.0 |
| DESeq2 | 1.46.0 |
| clusterProfiler | 4.14.6 |
| WGCNA | — |
| org.Hs.eg.db | 3.20.0 |
| AnnotationDbi | — |
| enrichplot | 1.26.6 |
| ggplot2 | 3.5.1 |
| pheatmap | 1.0.12 |
| tidyverse | 2.0.0 |
| RColorBrewer | 1.1.3 |
| ggrepel | — |

---

## How to Reproduce

1. Clone the repository
2. Download raw data from SRA (accession PRJNA320473)
3. Download GRCh38.p14 genome FASTA and GENCODE v47 GTF annotation
4. Update `project_dir` in each script's `setup` chunk to your local path
5. Run scripts in numerical order (00 → 08)

Scripts with resource-intensive steps (index building, alignment, DESeq2, WGCNA) use `eval=FALSE` by default. Change to `eval=TRUE` to execute.

---

## Project Structure

```
pipeline-rnaseq-luad-tfm/
├── scripts/
│   ├── 00_initial_setup.Rmd
│   ├── 01_quality_control.Rmd
│   ├── 02_genome_index_alignment.Rmd
│   ├── 03_quantification_featureCounts.Rmd
│   ├── 04_differential_expression_DESeq2.Rmd
│   ├── 05_functional_analysis.Rmd
│   ├── 06_gene_symbol_mapping.Rmd
│   ├── 07_WGCNA.Rmd
│   └── 08_figure_export.Rmd
├── data/
│   ├── Anexo_Top200_DEGs.csv
│   └── DEGs_con_simbolos_completo.csv
└── README.md
```

---

## Author

José Eduardo Hidalgo Suero
M.Sc. Biostatistics and Bioinformatics

---

## License

MIT
