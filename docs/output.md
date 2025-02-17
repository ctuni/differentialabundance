# nf-core/differentialabundance: Output

## Introduction

This document describes the output produced by the pipeline. The directories listed below will be created in the results directory after the pipeline has finished. All paths are relative to the top-level results directory.

## Report

This directory contains the main reporting output of the workflow.

<details markdown="1">
<summary>Output files</summary>

- `report/`
  - `*.html`: an HTML report file named according to the value of `params.study_name`, containing graphical and tabular summary results for the workflow run.

</details>

## Plots

Stand-alone graphical outputs are placed in this directory. They may be useful in external reporting, publication preparation etc.

<details markdown="1">
<summary>Output files</summary>

- `plots/`
  - `qc/`: Directory containing quality control plots from initial processing e.g. DESeq2
    - `*.png`
  - `exploratory/`: Directory containing standalone plots from exploratory analysis. Plots are stored in directories named for the main coloring variable used.
    - `[coloring variable]/png/boxplot.png`: Boxplot visualisation of abundance distributions
    - `[coloring variable]/png/density.png`: Density visualisation of abundance distributions
    - `[coloring variable]/png/pca2d.png`: 2-dimensional PCA plot
    - `[coloring variable]/png/pca3d.png`: 3-dimensional PCA plot
    - `[coloring variable]/png/sample_dendrogram.png`: A sample clustering dendrogram
    - `[coloring variable]/png/mad_correlation.png`: Outlier prediction plots using median absolute deviation (MAD)
  - `differential/`: Directory containing standalone plots from differential analysis. Plots are stored in directories named for the associated contrast.
    - `[contrast]/png/volcano.png`: Volcano plots of -log(10) p value agains log(2) fold changes
  - `gsea/`: Directory containing graphical outputs from GSEA (where enabled). Plots are stored in directories named for the associated contrast.
    - `[contrast]/png/[gsea_plot_type].png`

</details>

Most plots are included in the HTML report (see above), but are also included in static files in this folder to facilitate use in external reporting.

## Tables

<details markdown="1">
<summary>Output files</summary>

- `tables/`
  - `annotation1/`: Directory containing annotation matrices generated in the course of analysis
    - `[array platform].annotation.tsv`: Annotations derived from an array platform
    - `[GTF name].anno.tsv`: Species wise annotations derived from a GTF in RNA-seq analysis
  - `processed_abundance/`: Directory containing processed abundance values from initial processing from e.g. DESeq2 or Affy:
    - `[contrast_name].normalised_counts.tsv`: Normalised counts table (DESeq2)
    - `[contrast_name].vst.tsv`: Normalised counts table with a variance-stabilising transform (DESeq2)
    - `raw.matrix.tsv`: RMA background corrected matrix (Affy)
    - `normalised.matrix.tsv`: RMA background corrected and normalised intensities matrix (Affy)
  - `differential/`: Directory containing tables of differential statistics reported by differential modules such as DESeq2
    - `[contrast_name].deseq2.results.tsv`: Results of DESeq2 differential analyis (RNA-seq)
    - `OR [contrast_name].limma.results.tsv`: Results of Limma differential analyis (Affymetrix arrays)
  - `gsea/`: Directory containing tables of differential gene set analyis from GSEA (where enabled)
    - `[contrast]/[contrast].gsea_report_for_[condition].tsv`: A GSEA report table for each side of each contrast

</details>

The `differential` folder is likely to be the core result set for most users, containing the main tables of differential statistics.

## Shiny app

- `shinyngs_app/`
  - `[study name]`:
    - `data.rds`: serialized R object which can be used to generate a Shiny application
    - `app.R`: minimal R script that will source the data object and generate the app

The app must be run in an environment with [ShinyNGS](https://github.com/pinin4fjords/shinyngs) installed, or you can see the workflow parameters to deploy to shinyapps.io (see usage documentation).

<details markdown="1">
<summary>Output files</summary>

### Pipeline information

<details markdown="1">
<summary>Output files</summary>

- `pipeline_info/`
  - Reports generated by Nextflow: `execution_report.html`, `execution_timeline.html`, `execution_trace.txt` and `pipeline_dag.dot`/`pipeline_dag.svg`.
  - Reports generated by the pipeline: `pipeline_report.html`, `pipeline_report.txt` and `software_versions.yml`. The `pipeline_report*` files will only be present if the `--email` / `--email_on_fail` parameter's are used when running the pipeline.
  - Reformatted samplesheet files used as input to the pipeline: `samplesheet.valid.csv`.

</details>

[Nextflow](https://www.nextflow.io/docs/latest/tracing.html) provides excellent functionality for generating various reports relevant to the running and execution of the pipeline. This will allow you to troubleshoot errors with the running of the pipeline, and also provide you with other information such as launch commands, run times and resource usage.
