# 🧬 GWAS Harmonization, Mendelian Randomization & Machine Learning Pipeline

### 🔬 R-Based Computational Genomics Pipeline | Universidad Europea de Andalucía

**Author:** David Carro Vázquez, PhD  
**Research affiliation:** Universidad Europea de Andalucía (UEA), Spain  
**Programming language:** R  
**Research areas:** Genetic Epidemiology | GWAS | Mendelian Randomization | Causal Inference | Machine Learning | Healthy Aging

---

## 📖 Project Overview

This repository documents an R-based computational framework developed for the integration, harmonization, and analysis of large-scale genome-wide association study (GWAS) summary statistics.

The project investigates genetic relationships between physical activity, cardiometabolic traits, physiological characteristics, and aging-related outcomes through complementary statistical and causal inference approaches.

The pipeline integrates heterogeneous GWAS datasets into a standardized genetic analysis framework, combining:

- Large-scale GWAS data ingestion and SNP harmonization.
- Construction of a common SNP universe across multiple traits.
- Genetic variant quality control and effect-size validation.
- Generation of aligned SNP × trait matrices for machine-learning applications.
- Two-sample Mendelian Randomization (MR).
- Multivariable Mendelian Randomization (MVMR).
- Sensitivity analyses and genetic instrument validation.
- Bayesian colocalization analysis.
- SNP-level cross-trait screening and predictor prioritization.
- Exploratory linkage disequilibrium score regression (LDSC) automation.

The workflow is designed to support reproducible computational analyses of complex genetic relationships and potential causal determinants of healthy aging.

---

## 🎯 Research Objectives

1. Standardize heterogeneous GWAS summary-statistics datasets into a common analytical format.
2. Identify and harmonize shared genetic variants across multiple biological traits.
3. Construct aligned SNP-level effect-size matrices for statistical and machine-learning analyses.
4. Investigate potential causal relationships between biological exposures and aging-related outcomes using Mendelian Randomization.
5. Evaluate robustness through complementary MR estimators and sensitivity analyses.
6. Investigate whether exposure and outcome associations share underlying causal variants through colocalization.
7. Identify candidate biological predictors using cross-trait genetic effect-size screening.
8. Develop a scalable and documented computational framework for multi-trait GWAS integration.

---

## 🧪 GWAS Datasets and Biological Traits

The workflow integrates publicly available GWAS summary statistics spanning several biological domains.

### 🏃 Physical Activity and Accelerometry

- Moderate-to-vigorous physical activity (MVPA).
- Accelerometer-derived physical activity measures.
- Light-intensity physical activity.
- Total physical activity.
- Circadian activity characteristics.
- Walking duration and frequency.
- Self-reported physical activity.
- Leisure-time and sedentary behavior-related traits.

### ❤️ Cardiometabolic and Physiological Predictors

- Cardiorespiratory fitness and VO2max.
- HDL cholesterol.
- LDL cholesterol.
- Triglycerides.
- C-reactive protein.
- Glycated hemoglobin (HbA1c).
- Visceral adipose tissue.
- Total fat mass and fat-free mass.
- Waist-to-hip ratio adjusted for BMI.
- Waist circumference adjusted for BMI.
- Resting heart rate.
- White blood cell count.
- Lung function (FEV1).
- Bone mineral density.
- Hand grip strength.
- Chronotype.
- Smoking initiation.
- Dietary sugar intake.

### 🧓 Aging-Related Outcomes

The analytical framework includes three complementary aging-related outcomes:

- **Healthspan:** Genetic associations with the duration of life spent in relatively good health.
- **Parental lifespan:** A longevity-related phenotype based on parental survival.
- **Usual walking pace:** A functional phenotype related to physical performance.

These outcomes provide complementary perspectives on healthy aging, longevity, and physical function.

---

## ⚙️ Computational Analysis Pipeline

### 🔹 1. GWAS Data Import and Standardization

The pipeline implements a flexible GWAS reader designed to process heterogeneous summary-statistics formats.

**Main analytical steps:**

- Automatically discover GWAS files from predefined input directories.
- Import tabular GWAS datasets using memory-efficient `data.table` functions.
- Detect heterogeneous SNP identifier formats.
- Standardize key GWAS fields:
  - SNP identifier.
  - Effect allele (EA).
  - Other allele (OA).
  - Effect size (BETA).
  - Standard error (SE).
  - Effect allele frequency (EAF).
- Map dataset filenames to biologically interpretable trait names.
- Identify missing or incompatible input fields.
- Generate standardized data structures for downstream analyses.

### 🔹 2. Construction of a Common SNP Universe

A shared genetic variant reference is established using accelerometry GWAS datasets.

**Main analytical steps:**

- Define a reference SNP panel from accelerometry GWAS.
- Identify SNPs shared across the integrated datasets.
- Support SNP identifiers represented as rsIDs or chromosome-position coordinates.
- Convert compatible chromosome-position identifiers into rsIDs using a reference lookup.
- Remove duplicate SNP records.
- Restrict datasets to the common SNP intersection.
- Enforce consistent SNP ordering across traits.

This produces an aligned multi-trait genetic dataset suitable for comparative analyses.

### 🔹 3. SNP Quality Control and Harmonization Validation

The pipeline implements multiple validation procedures to evaluate the consistency of harmonized GWAS datasets.

**Main analytical steps:**

- Verify identical SNP sets across traits.
- Confirm consistent SNP ordering.
- Detect missing SNP identifiers and effect-size values.
- Identify duplicated variants.
- Evaluate SNP retention following harmonization.
- Examine effect-size distributions across traits.
- Compare directional concordance between biologically related traits.
- Audit the availability of allelic information, standard errors, allele frequencies, and sample-size metadata.
- Generate diagnostic tables and visualizations.

These procedures provide data-integrity checks before downstream modeling.

### 🔹 4. SNP × Trait Matrix Construction

The pipeline constructs a harmonized genetic effect-size matrix for machine-learning applications.

**Matrix structure:**

- **Rows:** Genetic variants (SNPs).
- **Columns:** GWAS traits.
- **Values:** GWAS effect-size estimates (BETA).

**Main analytical steps:**

- Extract harmonized SNP effect sizes across traits.
- Align all effect estimates to the same SNP reference.
- Construct a dense SNP × trait matrix.
- Validate missing values and matrix dimensions.
- Save intermediate and final objects as RDS files.
- Prepare the resulting matrix for downstream statistical learning.

This representation enables systematic comparison of genetic effect patterns across multiple phenotypes.

### 🔹 5. Memory-Efficient Data Processing

Large GWAS datasets can contain millions of genetic variants, requiring computationally efficient data handling.

The pipeline incorporates:

- Selective loading of required GWAS columns.
- Sequential processing of individual datasets.
- Intermediate RDS caching.
- Disk-based storage of harmonized trait objects.
- Explicit memory cleanup.
- Reuse of previously generated analytical objects.
- Modular execution of computationally intensive sections.

These procedures reduce repeated preprocessing and facilitate analysis of large genetic datasets.

### 🔹 6. Two-Sample Mendelian Randomization

The pipeline implements two-sample MR to investigate potential causal relationships between biological exposures and aging-related outcomes.

**Main analytical steps:**

- Select candidate genetic instruments.
- Apply instrument filtering and linkage disequilibrium clumping.
- Harmonize exposure and outcome alleles.
- Evaluate instrument strength.
- Estimate exposure-outcome associations using complementary MR estimators.

**Implemented methods include:**

- Inverse-variance weighted MR (IVW).
- MR-Egger regression.
- Weighted median estimation.
- Mode-based MR estimators.

The analysis generates causal effect estimates, uncertainty measures, and diagnostic outputs.

### 🔹 7. MR Sensitivity and Robustness Analyses

A comprehensive sensitivity framework is implemented to assess the robustness of MR findings.

**Main analytical steps:**

- Evaluate heterogeneity between genetic instruments.
- Examine directional horizontal pleiotropy.
- Perform MR-Egger sensitivity analyses.
- Apply Steiger directionality filtering.
- Conduct leave-one-out analyses.
- Apply MR-PRESSO where sufficient data and instruments are available.
- Evaluate instrument strength using F-statistics.
- Compare effect directions across complementary MR estimators.

**Generated visualizations include:**

- MR forest plots.
- Exposure-outcome effect grids.
- Leave-one-out diagnostic plots.
- Heterogeneity and pleiotropy summaries.
- Instrument strength tables.
- Cross-method robustness visualizations.

These analyses support interpretation of MR findings and help identify results sensitive to instrumental-variable assumptions.

### 🔹 8. Multivariable Mendelian Randomization (MVMR)

The workflow extends the causal inference framework to multivariable MR.

**Main analytical steps:**

- Construct exposure sets representing multiple biological predictors.
- Integrate genetic instruments across selected exposures.
- Estimate conditional exposure-outcome associations.
- Evaluate instrument strength and potential weak-instrument problems.
- Generate system-level MVMR summaries.
- Compare conditional estimates across exposure groups.

MVMR provides a complementary framework for investigating whether genetic associations remain after accounting for additional modeled exposures.

### 🔹 9. Bayesian Colocalization Analysis

The pipeline incorporates Bayesian colocalization to investigate whether exposure and outcome associations within genomic regions are compatible with a shared causal variant.

**Main analytical steps:**

- Identify genomic regions associated with candidate MR findings.
- Extract regional GWAS summary statistics.
- Apply approximate Bayes factor colocalization using `coloc.abf()`.
- Estimate posterior probabilities for alternative genetic association hypotheses.
- Evaluate evidence supporting a shared causal variant.
- Integrate colocalization results with MR estimates.
- Generate regional and summary visualizations.

**Colocalization hypotheses:**

- H0: Neither trait is associated with the region.
- H1: Only the first trait is associated.
- H2: Only the second trait is associated.
- H3: Both traits are associated through distinct causal variants.
- H4: Both traits share a causal variant.

Colocalization provides additional evidence relevant to the interpretation of MR results, subject to the assumptions of the colocalization model.

### 🔹 10. SNP Dimensionality Reduction for Machine Learning

The pipeline prepares high-dimensional genetic matrices for subsequent regularized regression analyses.

**Main analytical steps:**

- Calculate SNP-level variability across GWAS effect-size profiles.
- Rank variants according to cross-trait variability.
- Select a reduced set of informative SNPs.
- Generate a reduced SNP × trait matrix.
- Standardize predictor values.
- Save the reduced matrix for downstream modeling.

The workflow supports subsequent Elastic Net analyses, although preparation of the input matrix should be distinguished from fitting and validating a predictive model.

### 🔹 11. SNP-Level Genetic Effect Correlation Screening

Exploratory screening is performed to investigate relationships between GWAS effect-size profiles.

**Main analytical steps:**

- Calculate correlations between predictor and outcome SNP effect-size vectors.
- Evaluate correlation direction and magnitude.
- Compare associations across aging-related outcomes.
- Rank candidate biological predictors.
- Generate comparative summary tables.

These correlations are exploratory measures of shared SNP effect patterns and should not be interpreted as formal LD score regression estimates or causal effects.

### 🔹 12. Univariate SNP-Level Regression Screening

The pipeline implements univariate regression screening as a complementary method for prioritizing candidate predictors.

**Main analytical steps:**

- Model aging-outcome SNP effect sizes against individual predictor effect-size profiles.
- Estimate regression coefficients.
- Evaluate statistical associations and variance explained.
- Rank candidate predictors across outcomes.
- Compare regression-derived rankings with correlation-based screening.

### 🔹 13. Integrated Predictor Prioritization

The pipeline compares candidate predictors identified by complementary screening approaches.

**Main analytical steps:**

- Integrate correlation-based and regression-based rankings.
- Identify overlapping candidate predictors.
- Evaluate directional consistency.
- Generate Venn diagrams and comparative tables.
- Summarize prioritized traits for subsequent analyses.

### 🔹 14. Linkage Disequilibrium Score Regression Automation

An additional workflow section provides automation for genetic correlation analyses using LDSC.

**Main analytical steps:**

- Prepare GWAS summary statistics for LDSC.
- Interface with Python-based LDSC utilities.
- Configure reference LD scores.
- Execute genetic correlation analyses for selected trait pairs.
- Extract genetic correlation estimates, standard errors, and statistical significance values.

This section requires a separately installed LDSC environment and compatible reference data.

---

## 📂 Repository Structure

The GitHub repository contains:

```text
├── Proyecto1_GWASwEN.Rmd
├── Proyecto1_GWASwEN.html
├── README.md
└── requirements.txt
```

| File | Description |
|---|---|
| `Proyecto1_GWASwEN.Rmd` | R Markdown analytical workflow |
| `Proyecto1_GWASwEN.html` | Rendered analytical report |
| `README.md` | Project documentation |
| `requirements.txt` | Dependency information |

---

## 🧰 Technologies and R Packages

### 🧬 GWAS Data Processing

- R and R Markdown
- data.table
- dplyr
- tidyr
- stringr

### 🔬 Mendelian Randomization

- TwoSampleMR
- MRPRESSO
- MendelianRandomization

### 🧪 Colocalization and Genetic Analysis

- coloc
- LDSC (external Python-based workflow)

### 🤖 Machine Learning Preparation

- SNP effect-size matrix construction
- Variability-based feature filtering
- Predictor standardization
- Preparation for Elastic Net regression

### 📊 Visualization and Reporting

- ggplot2
- gridExtra
- DT
- knitr
- kableExtra
- patchwork

---

## ▶️ Reproducibility and Usage

The pipeline is implemented in R Markdown and organized into modular analytical sections.

To reproduce the workflow:

1. Install R and the required CRAN and Bioconductor packages.
2. Obtain the relevant GWAS summary-statistics datasets.
3. Configure the input and output directories.
4. Update the trait-to-file mappings where necessary.
5. Execute the GWAS ingestion and harmonization sections.
6. Generate and validate the shared SNP universe.
7. Construct the harmonized genetic effect-size matrices.
8. Execute the MR and sensitivity analysis sections.
9. Run colocalization and multivariable MR analyses where appropriate.
10. Perform SNP-level screening and predictor prioritization.
11. Review the generated diagnostic figures and statistical reports.

**Important:** Some computationally intensive R Markdown sections are configured with `eval = FALSE` and require manual execution or previously generated RDS objects.

The workflow also contains dataset-specific configuration paths and may require adaptation before running in a new environment.

---

## 💾 Intermediate Data and Computational Caching

The workflow saves intermediate datasets as RDS files to support modular execution and avoid repeated processing of large GWAS datasets.

Representative objects include:

- `accel_reference_snps.rds` — accelerometry-derived SNP reference panel.
- `common_snps_universe.rds` — SNPs shared across harmonized datasets.
- `gwas_list_final.rds` — harmonized GWAS datasets.
- `X_elastic_net.rds` — SNP × trait effect-size matrix.
- `gwas_mr.rds` — MR-ready summary-statistics object.

Additional objects store MR estimates, sensitivity analyses, instrument diagnostics, and downstream analytical results.

---

## 📊 Data Availability

Raw GWAS summary-statistics datasets and large intermediate genetic matrices are not included in this repository.

The analytical workflow is provided to document the computational methods and facilitate adaptation to compatible GWAS datasets.

Reproduction of the original analyses requires access to the corresponding GWAS sources and any necessary external reference datasets.

---

## 👨‍🔬 Author and Scientific Contributions

**David Carro Vázquez, PhD**

Computational researcher specializing in bioinformatics, statistical genomics, machine learning, and the integration of large-scale biological datasets.

This repository documents computational contributions to:

- Development of large-scale GWAS data ingestion and harmonization workflows.
- Construction of a standardized cross-trait SNP universe.
- Implementation of SNP quality-control and data-integrity procedures.
- Generation of genetic effect-size matrices for machine-learning applications.
- Implementation of two-sample Mendelian Randomization analyses.
- Development of sensitivity analysis and instrument validation workflows.
- Integration of multivariable MR and Bayesian colocalization.
- SNP-level statistical screening and candidate predictor prioritization.
- Memory-efficient data processing and intermediate-object caching.
- Generation of reproducible statistical reports and scientific visualizations.

The pipeline was developed in the context of computational genomics research at Universidad Europea de Andalucía, Spain.

---

## ⚠️ Methodological Considerations

- Mendelian Randomization estimates depend on the validity of instrumental-variable assumptions.
- Horizontal pleiotropy, sample overlap, weak instruments, and linkage disequilibrium may influence causal inference.
- Harmonization of SNP identifiers does not, by itself, guarantee correct alignment of effect alleles across GWAS.
- Colocalization results depend on regional variant coverage, prior assumptions, and the underlying causal-variant model.
- SNP-level effect-size correlations are exploratory and are not equivalent to genome-wide genetic correlation estimates from LDSC.
- Variability-based SNP selection is a preprocessing strategy rather than a validated predictive model.

---

## 📜 License

Please refer to the repository's `LICENSE` file, if provided, for applicable terms of use.

---

## 📬 Citation and Contact

**David Carro Vázquez, PhD**

GitHub: https://github.com/davicarro

For scientific inquiries or questions about the computational workflow, please contact the repository author through GitHub.
