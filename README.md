# Pipeline RNA-seq para Detección de Biomarcadores en Adenocarcinoma de Pulmón (LUAD)

## Descripción

Pipeline bioinformático reproducible para el análisis de datos RNA-seq orientado a la identificación de biomarcadores de expresión génica en adenocarcinoma de pulmón (LUAD). Este trabajo forma parte del Trabajo Fin de Máster (TFM) del Máster en Bioestadística y Bioinformática.

## Datos

- **Fuente:** Gene Expression Omnibus (GEO)
- **Proyecto:** PRJNA320473 / SRP074349
- **Muestras:** 20 (10 tejido normal + 10 tejido tumoral, diseño pareado)
- **Plataforma:** Illumina HiSeq 2500 (paired-end)
- **Genoma de referencia:** GRCh38.p14
- **Anotación:** GENCODE v47

## Estructura del Pipeline

| Script | Descripción |
|--------|-------------|
| `00_Verificacion_Inicial.Rmd` | Preparación del entorno y verificación de archivos |
| `01_Control_Calidad_FastQC.Rmd` | Control de calidad con FastQC y MultiQC |
| `02_Indice_Alineamiento_Rsubread.Rmd` | Construcción de índice y alineamiento al genoma |
| `03_Cuantificacion_featureCounts.Rmd` | Cuantificación de expresión génica |
| `04_Analisis_Diferencial_DESeq2.Rmd` | Análisis de expresión diferencial |
| `05_Analisis_Funcional.Rmd` | Enriquecimiento funcional (GO, KEGG, GSEA) |

## Archivos de Resultados

El repositorio incluye archivos CSV con los resultados del análisis de expresión diferencial:

| Archivo | Contenido |
|---------|-----------|
| `DEGs_con_simbolos_completo.csv` | Lista completa de genes diferencialmente expresados |
| `Anexo_Top200_DEGs.csv` | Lista de los 200 primeros genes diferencialmente expresados |

## Requisitos

### Software
- R versión 4.4.2
- RStudio
- FastQC 0.12.1
- MultiQC 1.27

### Paquetes de R/Bioconductor
- Rsubread 2.20.0
- DESeq2 1.46.0
- clusterProfiler 4.14.6
- org.Hs.eg.db 3.20.0
- AnnotationDbi
- enrichplot 1.26.6
- ggplot2 3.5.1
- pheatmap 1.0.12
- tidyverse 2.0.0
- RColorBrewer 1.1.3

## Resultados Principales

- **DEGs identificados:** 6,989 (4,328 sobreexpresados, 2,661 subexpresados)
- **Rango log2FC:** -7.40 a 22.79
- **Términos GO enriquecidos:** 1,384
- **Vías KEGG enriquecidas:** 38
- **GSEA:** 585 términos GO, 50 vías KEGG

### Genes destacados
- **Sobreexpresados:** CSN1S1, PADI3, MMP13, COL11A1
- **Subexpresados:** SLC6A4, ITLN1, CA4

## Uso

1. Clonar el repositorio
2. Descargar datos de SRA (PRJNA320473)
3. Descargar genoma de referencia GRCh38.p14 y anotación GTF
4. Ejecutar los scripts en orden numérico

## Autor

José Eduardo Hidalgo Suero

## Licencia

Este proyecto está bajo la licencia MIT.
