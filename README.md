# Mendelian Randomization Pipeline

This repository contains a reproducible pipeline for large-scale Mendelian Randomization (MR) analyses integrating GWAS summary statistics and machine learning approaches.

## Overview

The workflow is designed to:

* Harmonize multiple GWAS datasets into a common SNP universe
* Perform stringent SNP-level quality control
* Construct predictor matrices for downstream modeling
* Apply Elastic Net regularization for feature selection
* Conduct two-sample Mendelian Randomization analyses
* Perform sensitivity analyses (Egger, Weighted Median, MR-PRESSO, Leave-one-out)
* Support colocalization analyses

## Pipeline Structure

* `MR_pipeline_UKB_Accelerometry.Rmd`
  Full end-to-end analysis workflow, including:

  * GWAS ingestion and harmonization
  * SNP QC and alignment
  * Elastic Net modeling
  * MR analysis and sensitivity testing
  * Visualization and reporting

* `requirements.txt`
  List of required R packages and dependencies

## Methods

This pipeline integrates:

* Elastic Net regression (glmnet) for SNP prioritization
* Two-sample Mendelian Randomization framework
* LD clumping and instrument filtering
* Sensitivity analyses to ensure robustness of causal estimates

## Reproducibility

All intermediate datasets are cached as `.rds` objects to ensure:

* Reproducibility
* Computational efficiency
* Modular workflow execution

## Author

David Carro Vázquez
Postdoctoral Researcher
University of California San Francisco (UCSF)
University of East Anglia (UEA)

## Notes

Large GWAS datasets are not included in this repository due to size constraints.
