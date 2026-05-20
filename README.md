# MetaElasto

MetaElasto is the code repository associated with a Master's Thesis project on the integration of torsional wave elastography, viscoelastic modelling and computational analysis for the study of metabolic and cardiometabolic alterations.

The project focuses on the analysis of torsional wave elastography measurements acquired in superficial tissues, with special attention to subcutaneous adipose tissue, frequency-resolved signal information, protocol-dependent variability, missing data patterns and interpretable modelling strategies.

The work is methodological and exploratory. It does not aim to provide a validated diagnostic tool. Instead, it builds a reproducible analytical framework to investigate whether mechanical information extracted from torsional wave elastography signals may be useful as a candidate source of non-invasive biomarkers in a cardiometabolic context.

## Project context

Metabolic diseases such as obesity, type 2 diabetes and metabolic syndrome are usually evaluated through clinical, anthropometric and biochemical markers. These markers are essential, but they do not directly describe the mechanical behaviour of superficial tissues.

Subcutaneous adipose tissue is biologically active and can undergo structural and functional changes in obesity and cardiometabolic disease, including inflammation, extracellular matrix remodelling and fibrosis. These changes may affect tissue mechanics. For this reason, the project explores whether torsional wave elastography can provide additional information about tissue status beyond conventional clinical variables.

Torsional wave elastography is especially relevant for this purpose because it allows the recorded wave response to be analysed at signal level. Instead of reducing the acquisition immediately to a single scalar stiffness value, the workflow preserves frequency-dependent information and waveform morphology. This makes it possible to study mechanical and viscoelastic descriptors in a more detailed and interpretable way.

## Main objective

The main objective of this repository is to document the computational workflow used to analyse torsional wave elastography data in relation to cardiometabolic variables.

The analysis aims to

- organise raw elastography signal files into a harmonised structure
- preserve frequency-resolved waveform information
- link elastography recordings with acquisition metadata
- integrate mechanical descriptors with clinical and anthropometric variables
- assess signal quality and acquisition consistency
- derive candidate mechanical and viscoelastic descriptors
- study missing data patterns in physical and viscosity-related variables
- explore protocol-dependent and anatomical-site-dependent variability
- evaluate associations with cardiometabolic endpoints
- compare interpretable statistical and machine-learning formulations
- document methodological limitations and future lines of work

## Scientific scope

The project is centred on the methodological question of how torsional wave elastography data should be processed, structured and analysed before making any clinical interpretation.

The repository therefore prioritises transparency, traceability and interpretability over the search for highly optimised predictive models. This is important because the dataset contains repeated measurements, different acquisition protocols, multiple anatomical sites and heterogeneous signal quality. Under these conditions, strong predictive performance can be misleading if it is not supported by careful data harmonisation, quality control and leakage-aware validation.

## Data and study design

The analysis is based on an existing torsional wave elastography dataset acquired within a broader cardiometabolic research framework.

The available information includes

- raw torsional wave elastography signal files
- acquisition metadata
- protocol information
- anatomical-site information
- repeated measurements within subject and site
- derived physical and viscoelastic variables
- clinical and anthropometric variables
- cardiometabolic risk-factor variables

The analytical unit is constructed at subject, timepoint and anatomical-site level, while preserving acquisition-level provenance whenever possible.

The original dataset includes measurements from different anatomical regions such as abdomen, arm and leg. The workflow also distinguishes between old-code and new-code acquisition branches, because protocol differences may influence signal structure, frequency coverage, repeated-measurement patterns and downstream modelling results.

## Analytical strategy

The project follows a signal-level analytical strategy.

Raw signal files are parsed and converted into structured acquisition-level records. Each acquisition is described by patient identifiers, protocol version, anatomical site, measurement index, source filename, acquisition date and available frequency channels.

Frequency channels are not forced into a single sparse table at the beginning of the workflow. Instead, each acquisition preserves its frequency-resolved signal arrays, while long-format summaries are generated when needed for downstream analysis.

This design allows the analysis to remain flexible across protocols with different frequency grids and different numbers of repeated acquisitions.

## Main workflow

The computational workflow is organised into several stages.

### 1. Signal ingestion and parsing

Raw torsional wave elastography files are read and parsed according to their filename structure.

The workflow extracts

- protocol version
- local and global patient identifiers
- anatomical site code
- measurement index within site
- acquisition timestamp
- source file information
- available frequencies
- signal arrays for each frequency

### 2. Metadata harmonisation

Elastography metadata are standardised and linked to the signal-level records.

This step is used to assign

- hospital patient identifiers
- study timepoints
- protocol-specific information
- acquisition-level provenance

The harmonisation step is designed to maintain traceability between raw files, metadata and the final analytical tables.

### 3. Clinical data integration

Clinical and anthropometric variables are harmonised into a long-format structure and merged with the elastography records.

The clinical variables used in the analysis include cardiometabolic markers such as

- waist circumference
- triglycerides
- HDL cholesterol
- systolic blood pressure
- diastolic blood pressure
- glucose
- age
- sex

Derived cardiometabolic flags are then created from these variables.

### 4. Cardiometabolic endpoint construction

The workflow defines binary and composite cardiometabolic endpoints.

These include individual risk-factor indicators such as

- abdominal obesity
- high triglycerides
- low HDL cholesterol
- hypertension
- high glucose

A composite metabolic syndrome endpoint is also constructed from the combination of these criteria.

### 5. Signal-quality assessment

Signal quality is evaluated through acquisition-level and block-level metrics.

The quality-control strategy considers

- number of available frequency channels
- waveform amplitude
- RMS signal magnitude
- peak-to-peak amplitude
- drift-related indicators
- roughness-related indicators
- similarity to patient-site-timepoint reference waveforms
- correlation with repeated acquisitions
- normalised error with respect to block-level references

The goal is not to remove large amounts of data aggressively, but to identify clearly problematic acquisitions while preserving borderline cases for sensitivity analysis.

### 6. Conservative filtering

Acquisitions are classified into three categories.

- `keep`
- `review`
- `exclude`

Only acquisitions with clear structural problems or multiple adverse quality indicators are excluded automatically. This conservative approach allows the impact of quality control on sample size and dataset balance to be quantified before statistical analysis and modelling.

### 7. Feature construction

The workflow combines several types of features.

These include

- physics-derived mechanical variables
- viscoelastic descriptors
- signal-derived morphology summaries
- quality-control descriptors
- frequency-specific waveform summaries
- clinical and anthropometric variables
- binary cardiometabolic flags

Particular attention is given to variables such as wave-speed-related descriptors, viscosity-related descriptors and their associated uncertainty or variability measures.

### 8. Missing data analysis

Missing data are treated as an important methodological result rather than only as a technical inconvenience.

The analysis examines whether missingness affects specific physical variables, especially viscosity-related and derived mechanical parameters. This is relevant because non-random missingness may indicate that some descriptors are less robust under certain acquisition conditions, protocols, anatomical sites or signal-quality regimes.

The repository therefore supports the documentation of

- which variables are more complete
- which variables are more unstable
- whether missingness differs across protocols
- whether missingness differs across anatomical sites
- how missingness affects modelling decisions
- which variables should be interpreted cautiously

### 9. Exploratory multivariate analysis

Exploratory multivariate methods are used to study the internal structure of the mechanical and signal-derived variables.

These analyses include

- descriptive summaries
- correlation analysis
- principal component analysis
- clustering
- protocol-aware visualisation
- site-aware visualisation
- comparison of cardiometabolic groups

The clustering analysis is interpreted cautiously because observed structure may reflect acquisition protocol, anatomical site or measurement conditions, not only biological variation.

### 10. Protocol-aware analysis

The repository explicitly considers differences between acquisition protocols.

This is important because protocol effects may influence

- available frequency channels
- number of repeated measurements
- signal amplitude
- waveform morphology
- physical descriptor availability
- missing data patterns
- apparent clustering structure
- model performance

For this reason, several analyses are performed separately by protocol or are interpreted with protocol as a central methodological factor.

### 11. Frequency-wise analysis

Frequency-resolved analysis is one of the main motivations of the project.

Instead of collapsing all signal information into a single global descriptor, the workflow studies whether specific frequencies, anatomical sites or protocol-site-frequency combinations show stronger relationships with cardiometabolic variables.

This is particularly relevant for glucose-related analyses, where some frequency-specific waveform summaries may provide more informative patterns than broad composite endpoints.

### 12. Predictive modelling

The modelling stage compares several analytical formulations.

The project includes classical and exploratory models such as

- logistic regression
- random forests
- protocol-stratified models
- feature-block comparisons
- targeted site-frequency models
- raw-waveform temporal models
- temporal convolutional network approaches

The aim is not only to maximise performance, but to compare whether different model families provide stable, interpretable and methodologically coherent results.

### 13. Validation and leakage control

The workflow gives special attention to internal validation.

Because repeated acquisitions may exist for the same subject, validation must avoid information leakage between training and testing partitions. Subject-level separation is therefore important when evaluating out-of-subject generalisation.

The repository documents validation decisions so that reported performance is not inflated by repeated measurements, duplicated information or preprocessing steps that use information from the full dataset before splitting.

## Repository structure

```text
MetaElasto/
├── README.md
├── Code_Report.pdf
└── notebooks/
    ├── 00_full_analysis.ipynb
    ├── 01_preprocessing.ipynb
    ├── 02_descriptive_audit.ipynb
    ├── 03_signal_quality_control.ipynb
    ├── 04_statistical_analysis.ipynb
    ├── 05_machine_learning.ipynb
    └── 06_deep_learning.ipynb
```

## Repository contents

### `README.md`

Provides a general description of the project, its methodological scope, the organisation of the repository, data availability restrictions and reproducibility notes.

### `Code_Report.pdf`

Contains a static exported version of the computational workflow.

This file is included as supplementary documentation for review purposes. It provides a complete view of the code and analytical process in PDF format, while the notebooks in the `notebooks/` folder provide a more navigable version divided into thematic blocks.

### `notebooks/`

Contains the notebook-based implementation of the analytical workflow.

The original analysis was developed as a single notebook and then divided into thematic notebooks to improve readability, traceability and reviewability. Each notebook corresponds to one methodological block of the thesis. The complete notebook is also preserved to show the full analytical workflow in a single file.

#### `00_full_analysis.ipynb`

Contains the complete analytical workflow.

This notebook provides the full sequence of the project, from data loading and harmonisation to quality control, statistical analysis, machine learning and deep-learning experiments. It is kept as a transparent record of the full computational process.

#### `01_preprocessing.ipynb`

Contains the preprocessing and data-harmonisation workflow.

This notebook reads and organises the raw torsional wave elastography signal files, parses old-code and new-code acquisition formats, extracts metadata from filenames, assigns patient and timepoint information, and links signal-level records with elastograph metadata and clinical tables.

The main output of this block is the harmonised acquisition-level dataset used in the rest of the analysis.

#### `02_descriptive_audit.ipynb`

Contains the descriptive audit of the harmonised dataset.

This notebook summarises the structure of the data by protocol, patient, timepoint and anatomical site. It also evaluates frequency coverage, acquisition counts, repeated-measurement structure and basic signal properties before applying any exclusion criteria.

The purpose of this block is to understand the dataset structure and identify potential inconsistencies before formal quality control.

#### `03_signal_quality_control.ipynb`

Contains the signal-quality assessment and conservative filtering strategy.

This notebook computes acquisition-level quality metrics from the frequency-resolved waveforms and classifies acquisitions into `keep`, `review` and `exclude` categories.

The quality-control strategy is intentionally conservative. Its goal is to identify clearly problematic acquisitions while preserving borderline cases for later sensitivity analysis.

#### `04_statistical_analysis.ipynb`

Contains the main statistical and exploratory analyses.

This notebook studies the distribution of mechanical, signal-derived and clinical variables. It includes descriptive statistics, group comparisons, correlation analyses, missing-data exploration, protocol-aware summaries and exploratory multivariate analyses such as PCA and clustering.

The objective of this block is to evaluate whether the extracted mechanical descriptors show interpretable patterns in relation to anatomical site, protocol and cardiometabolic variables.

#### `05_machine_learning.ipynb`

Contains the classical machine-learning analyses.

This notebook compares interpretable supervised models using different feature blocks and target definitions. The analysis focuses on internal validation, protocol-aware modelling, performance comparison and the stability of results.

The aim is not only to maximise predictive performance, but to assess whether the available descriptors provide robust and interpretable information for cardiometabolic classification tasks.

#### `06_deep_learning.ipynb`

Contains exploratory deep-learning analyses based on waveform information.

This notebook evaluates whether raw or minimally processed torsional wave elastography signals contain useful temporal information that may not be fully captured by handcrafted descriptors.

These models are treated as exploratory and are interpreted cautiously, especially because of sample-size limitations, repeated measurements and the need to avoid information leakage.

## Data availability

The original biomedical dataset is not publicly available.

The data are excluded from this repository because they may contain sensitive clinical or research information. Full reproduction of the analyses requires authorised access to the protected dataset.

The repository is intended to document the analytical workflow without exposing confidential information.

Where possible, the notebooks preserve the methodological structure of the workflow so that the code can be inspected and understood even when the protected dataset is not available.

## Reproducibility

The notebooks are provided for methodological transparency.

Some parts of the workflow may not run without access to the original protected dataset. However, the repository documents the main analytical decisions, preprocessing steps, quality-control procedures, statistical analyses and modelling comparisons used in the thesis.

The workflow is designed to be reproducible under the same data-access conditions.

## Current status

This repository is under active development.

The current priorities are

- cleaning the notebooks
- removing local paths and private information
- checking that no sensitive data are uploaded
- improving the documentation of each analytical block
- adding a complete `requirements.txt` file if needed
- aligning the repository with the final version of the thesis

## Requirements

The project was developed in Python using a notebook-based workflow.

Core dependencies include

```text
numpy
pandas
scipy
scikit-learn
matplotlib
seaborn
jupyter
```

Additional dependencies may be required for specific modelling steps, deep-learning experiments or notebook execution.

A complete `requirements.txt` file may be added to document the final computational environment.

## How to use this repository

Clone the repository.

```bash
git clone https://github.com/<username>/MetaElasto.git
cd MetaElasto
```

Open the notebook folder.

```bash
cd notebooks
```

Open the complete workflow.

```bash
jupyter notebook 00_full_analysis.ipynb
```

Alternatively, open each analytical block separately.

```bash
jupyter notebook 01_preprocessing.ipynb
jupyter notebook 02_descriptive_audit.ipynb
jupyter notebook 03_signal_quality_control.ipynb
jupyter notebook 04_statistical_analysis.ipynb
jupyter notebook 05_machine_learning.ipynb
jupyter notebook 06_deep_learning.ipynb
```

Full execution requires access to the protected dataset and the correct local configuration of input paths.

## Methodological limitations

The project should be interpreted as an exploratory and methodological analysis.

Important limitations include

- absence of public access to the original dataset
- heterogeneous acquisition protocols
- repeated measurements within subjects and sites
- possible protocol-induced structure in clustering
- missing data in some physical and viscosity-related variables
- limited effective sample size for some protocol-site-target combinations
- internal validation only
- absence of external validation
- exploratory nature of the predictive modelling results

These limitations are part of the scientific interpretation of the work and are documented to avoid overstating the clinical meaning of the results.

## Main contribution

The main contribution of MetaElasto is not a final diagnostic model, but a transparent computational framework for analysing torsional wave elastography data in a cardiometabolic setting.

The repository supports the thesis by documenting how raw signal files are transformed into structured analytical data, how mechanical and clinical variables are linked, how quality control is performed, how protocol effects are considered and how exploratory statistical and modelling analyses are evaluated.

## Author

Antoni Ignasi Cànaves Llabrés

Master's Thesis project  
Master's Degree in Bioinformatics and Biostatistics  
Universitat Oberta de Catalunya

## Disclaimer

This repository is intended for academic documentation and methodological transparency.

The code is shared for evaluation and research-documentation purposes. It does not include raw clinical data, identifiable information or protected research data.

The analyses presented here should not be interpreted as a validated clinical diagnostic system.
