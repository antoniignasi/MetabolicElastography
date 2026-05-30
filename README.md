# MetabolicElastography

MetabolicElastography is the code repository associated with the Master's Thesis entitled *Integration of torsional wave elastography and computational models for the exploratory assessment of cardiometabolic alterations*.

The project focuses on the computational analysis of torsional wave elastography (TWE) measurements acquired at superficial tissue sites, with special attention to subcutaneous adipose tissue. The workflow preserves frequency-resolved signal information, integrates mechanical and viscoelastic descriptors with clinical and anthropometric variables, and explicitly considers protocol-dependent variability, missingness, signal quality, anatomical-site effects, and leakage-aware internal modelling.

The work is methodological and exploratory. It does not aim to provide a validated diagnostic tool or a clinically deployable prediction system. Instead, it builds a reproducible analytical framework to investigate whether information extracted from TWE signals may provide useful candidate descriptors of superficial tissue behaviour in a cardiometabolic context.

## Project context

Metabolic diseases such as obesity, type 2 diabetes and metabolic syndrome are usually evaluated through clinical, anthropometric and biochemical markers. These markers are essential for clinical characterisation, but they do not directly describe the mechanical behaviour of superficial tissues.

Adipose tissue and adjacent superficial structures can undergo structural and functional changes in obesity and cardiometabolic disease, including inflammation, extracellular matrix remodelling, fibrosis and glycation-related alterations. These processes may affect tissue mechanics. For this reason, the project explores whether TWE can provide complementary information about superficial tissue state beyond conventional clinical variables.

TWE is especially relevant for this purpose because it allows the recorded wave response to be analysed at signal level. Rather than reducing the acquisition immediately to a single scalar stiffness estimate, the workflow preserves frequency-dependent information and waveform morphology. This makes it possible to examine candidate mechanical, viscoelastic and signal-derived descriptors in a more detailed and interpretable way.

## Main objective

The main objective of this repository is to document the computational workflow used to analyse TWE data in relation to cardiometabolic variables.

The analysis aims to:

- organise raw elastography signal files into a harmonised structure;
- preserve frequency-resolved waveform information;
- link elastography recordings with acquisition metadata and study timepoints;
- integrate mechanical descriptors with clinical and anthropometric variables;
- assess signal quality and acquisition consistency;
- derive candidate mechanical, viscoelastic and signal-derived descriptors;
- characterise missingness and instability in selected physical variables;
- explore protocol-dependent and anatomical-site-dependent variability;
- evaluate exploratory associations with cardiometabolic endpoints;
- compare interpretable statistical, classical machine-learning and raw-waveform modelling approaches;
- apply participant-separated internal evaluation procedures when predictive models are trained;
- interpret deep-learning results as exploratory internal comparisons rather than as definitive clinical validation;
- document methodological limitations and future lines of work.

## Scientific scope

The project is centred on the methodological question of how TWE data should be processed, structured and analysed before making any clinical interpretation.

The repository therefore prioritises transparency, traceability and interpretability over the search for highly optimised predictive models. This is important because the dataset contains repeated measurements, different acquisition protocol branches, multiple anatomical sites and heterogeneous signal-quality characteristics. Under these conditions, apparently strong predictive performance can be misleading if it is not supported by careful data harmonisation, quality control and participant-separated validation.

The analyses presented in this repository should therefore be understood as exploratory and hypothesis-generating. Their purpose is to identify potentially informative signal representations and protocol-site-frequency configurations that may justify future investigation under stricter validation designs.

## Data and study design

The analysis is based on an existing TWE dataset acquired within the TEMPUS cardiometabolic research framework.

The available information includes:

- raw torsional wave elastography signal files;
- acquisition metadata;
- protocol information;
- anatomical-site information;
- repeated measurements within participants and sites;
- reconstructed physical and viscoelastic variables;
- clinical and anthropometric variables;
- cardiometabolic risk-factor variables.

The principal analytical unit is constructed at participant, protocol, timepoint and anatomical-site level after aggregation of repeated acquisitions. Acquisition-level provenance is nevertheless preserved for quality-control procedures, waveform inspection and frequency-wise exploratory analyses.

The original dataset includes measurements acquired from several anatomical regions, including:

- abdomen;
- arm;
- leg.

The workflow distinguishes between `old-code` and `new-code` protocol branches because these structures differ in frequency coverage, repeated-measurement organisation, signal characteristics and availability of reconstructed physical variables. Protocol version is therefore treated as a central methodological factor rather than as a negligible technical detail.

## Analytical strategy

The project follows a signal-level analytical strategy.

Raw signal files are parsed and converted into structured acquisition-level records. Each acquisition is described by participant identifiers, protocol version, anatomical site, measurement index, source filename, acquisition information and the available frequency channels.

Frequency channels are not forced into a single sparse table at the beginning of the workflow. Instead, each acquisition preserves its frequency-resolved signal arrays, while lighter long-format or aggregated representations are generated when required for descriptive analysis, statistical testing or modelling.

This design allows the workflow to remain flexible across protocol branches with different frequency grids and different repeated-acquisition structures, while preserving the provenance of the original signals.

## Main workflow

The computational workflow is organised into thirteen main stages.

### 1. Signal ingestion and parsing

Raw TWE files are read and parsed according to their filename and protocol structure.

The workflow extracts:

- protocol version;
- local and global participant identifiers;
- anatomical-site code;
- measurement index within site;
- acquisition information;
- source file information;
- available frequencies;
- signal arrays for each frequency.

### 2. Metadata harmonisation

Elastography metadata are standardised and linked to the signal-level records.

This stage is used to assign or harmonise:

- hospital participant identifiers;
- study timepoints;
- protocol-specific information;
- acquisition-level provenance;
- consistent site and variable naming conventions.

The harmonisation step is designed to maintain traceability between raw files, metadata and the final analytical tables.

### 3. Clinical data integration

Clinical and anthropometric variables are harmonised into a longitudinal structure and merged with the elastography records.

The clinical variables incorporated into the analytical workflow include cardiometabolic measurements such as:

- waist circumference;
- triglycerides;
- HDL cholesterol;
- systolic blood pressure;
- diastolic blood pressure;
- glucose;
- age;
- sex.

These variables provide the clinical and biological context required for the interpretation of the TWE-derived descriptors.

### 4. Cardiometabolic endpoint construction

The workflow defines individual and composite cardiometabolic endpoints.

Individual binary indicators include:

- abdominal obesity;
- high triglycerides;
- low HDL cholesterol;
- hypertension;
- high glucose.

A composite metabolic-syndrome endpoint is also constructed from the combination of these criteria.

The analyses later compare the behaviour of broad syndrome-level endpoints with more specific glucose-related outcomes.

### 5. Signal-quality assessment

Signal quality is evaluated through acquisition-level and block-level descriptors.

The quality-control strategy considers:

- number of available frequency channels;
- waveform amplitude;
- RMS signal magnitude;
- peak-to-peak amplitude;
- drift-related indicators;
- roughness-related indicators;
- similarity to participant-site-timepoint reference waveforms;
- correlation with repeated acquisitions;
- normalised error with respect to block-level references.

The aim is not to remove large amounts of data aggressively, but to identify clearly problematic acquisitions while preserving borderline observations for cautious interpretation and sensitivity-oriented analyses.

### 6. Conservative filtering

Acquisitions are classified into three categories:

- `keep`;
- `review`;
- `exclude`.

Only acquisitions with clear structural problems or sufficiently adverse quality indicators are excluded automatically. This conservative strategy makes it possible to quantify the impact of quality control on sample size, protocol distribution and downstream analytical structure before proceeding to statistical analysis and modelling.

### 7. Feature construction

The workflow combines several types of features:

- physics-derived mechanical variables;
- viscosity-related and viscoelastic descriptors;
- signal-derived morphology summaries;
- quality-control descriptors;
- frequency-specific waveform summaries;
- clinical and anthropometric variables;
- binary cardiometabolic flags.

Particular attention is given to wave-speed-related descriptors, viscosity-related descriptors, waveform amplitude measures, RMS summaries and their associated variability or uncertainty measures.

These variables are treated as candidate analytical descriptors rather than as clinically validated biomarkers.

### 8. Missing-data characterisation

Missingness is treated as an important methodological result rather than only as a technical inconvenience.

The analysis examines whether missing or unstable values affect specific reconstructed physical variables, especially viscosity-related and other derived mechanical quantities. This is relevant because non-random missingness may indicate that some descriptors are less robust under particular protocol branches, anatomical sites or signal-quality regimes.

The repository documents:

- which variables are more complete;
- which variables show greater instability;
- whether missingness differs across protocol branches;
- whether missingness differs across anatomical sites;
- how missingness influences analytical decisions;
- which descriptors require cautious interpretation.

### 9. Exploratory multivariate analysis

Exploratory multivariate methods are used to study the internal structure of the mechanical and signal-derived variables.

These analyses include:

- descriptive summaries;
- correlation analysis;
- principal component analysis;
- clustering;
- protocol-aware visualisation;
- site-aware visualisation;
- comparison with cardiometabolic groupings.

The clustering analysis is interpreted cautiously because observed structure may reflect acquisition protocol, anatomical site, signal regime or measurement conditions rather than biological variation alone.

### 10. Protocol-aware analysis

The repository explicitly considers differences between acquisition protocol branches.

Protocol effects may influence:

- available frequency channels;
- number of repeated measurements;
- signal amplitude;
- waveform morphology;
- reconstructed physical-variable availability;
- missingness patterns;
- apparent clustering structure;
- model performance.

For this reason, several analyses are conducted separately by protocol or are interpreted with protocol version as a central methodological factor.

### 11. Frequency-wise exploratory analysis

Frequency-resolved analysis is one of the main motivations of the project.

Rather than collapsing all signal information into a single global descriptor, the workflow studies whether specific frequencies, anatomical sites or protocol-site-frequency combinations show stronger relationships with cardiometabolic variables.

This approach is particularly relevant for glucose-related analyses, where selected frequency-specific waveform summaries showed more coherent exploratory patterns than the broader metabolic-syndrome endpoint.

Because the frequency-wise screening analyses are performed at acquisition level, repeated measurements from the same participant may contribute correlated observations. Therefore, the corresponding association statistics are interpreted as exploratory indicators for identifying promising protocol-site-frequency patterns rather than as confirmatory evidence of independent associations.

### 12. Predictive modelling

The modelling stage compares several analytical formulations.

The project includes classical and exploratory approaches such as:

- logistic regression;
- random forests;
- protocol-stratified models;
- feature-block comparisons;
- targeted site-frequency models;
- raw-waveform convolutional neural networks;
- temporal convolutional network approaches.

The aim is not only to maximise predictive performance, but to examine whether different signal representations and model families provide stable, interpretable and methodologically coherent results.

The deep-learning stage is exploratory. Candidate raw-waveform and temporal configurations were compared using internal test-partition results in order to identify promising signal representations. Therefore, the strongest observed temporal convolutional network configuration should be interpreted as a hypothesis-generating candidate for future validation rather than as a definitively validated predictive model.

### 13. Validation and leakage control

The workflow gives special attention to internal validation.

Because repeated acquisitions exist for the same participant, evaluation procedures must avoid information leakage between training and evaluation partitions. Participant-level separation is therefore essential when assessing out-of-participant generalisation.

The repository documents validation decisions so that reported performance is not inflated by repeated measurements, duplicated information or preprocessing steps that use information from the full dataset before splitting. In the deep-learning experiments, participant-level separation was preserved between training, validation and internal test partitions.

However, candidate raw-waveform and temporal configurations were explored using internal test-partition results. Consequently, their performance estimates are interpreted as exploratory internal comparisons rather than as a definitive independent assessment of generalisation. A confirmatory assessment would require a prospectively reserved final test cohort, nested validation or external validation data.

## Repository structure

```text
MetabolicElastography/
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

Provides a general description of the project, its methodological scope, the organisation of the repository, data-availability restrictions, reproducibility considerations and main limitations.

### `Code_Report.pdf`

Contains a static exported version of the computational workflow.

This file is included as supplementary documentation for review purposes. It provides an overview of the code and analytical process in PDF format, while the notebooks in the `notebooks/` folder provide a more navigable version divided into thematic analytical blocks.

### `notebooks/`

Contains the notebook-based documentation and implementation of the analytical workflow.

The original analysis was developed as a complete notebook and was subsequently divided into thematic notebooks to improve readability, traceability and reviewability. Each notebook corresponds to one principal methodological block of the thesis. The complete notebook is also preserved as a reference representation of the full computational workflow.

#### `00_full_analysis.ipynb`

Contains the complete analytical workflow.

This notebook records the full sequence of the project, from data loading and harmonisation to quality control, statistical analysis, classical machine learning and exploratory deep-learning experiments. It is preserved as a transparent reference of the complete computational process.

#### `01_preprocessing.ipynb`

Contains the preprocessing and data-harmonisation workflow.

This notebook reads and organises the raw TWE signal files, parses the `old-code` and `new-code` acquisition formats, extracts metadata from filenames, assigns participant and timepoint information, and links signal-level records with elastograph metadata and clinical tables.

The main output of this block is the harmonised acquisition-level dataset used in later stages of the analysis.

#### `02_descriptive_audit.ipynb`

Contains the descriptive audit of the harmonised dataset.

This notebook summarises the structure of the data by protocol, participant, timepoint and anatomical site. It also evaluates frequency coverage, acquisition counts, repeated-measurement structure and basic signal properties before applying exclusion criteria.

The purpose of this block is to understand the dataset architecture and identify relevant structural characteristics before formal quality control and downstream interpretation.

#### `03_signal_quality_control.ipynb`

Contains the signal-quality assessment and conservative filtering strategy.

This notebook computes acquisition-level quality metrics from the frequency-resolved waveforms and classifies acquisitions into `keep`, `review` and `exclude` categories.

The quality-control strategy is intentionally conservative. Its aim is to identify clearly problematic acquisitions while preserving borderline cases and retaining most of the original analytical structure.

#### `04_statistical_analysis.ipynb`

Contains the main statistical and exploratory analyses.

This notebook examines the distribution of mechanical, signal-derived and clinical variables. It includes descriptive statistics, group comparisons, correlation analyses, missing-data exploration, protocol-aware summaries, PCA, clustering and frequency-wise exploratory analyses.

The objective of this block is to evaluate whether the extracted descriptors show interpretable patterns in relation to anatomical site, protocol structure and cardiometabolic variables, while avoiding overinterpretation of exploratory findings.

#### `05_machine_learning.ipynb`

Contains the classical machine-learning analyses.

This notebook compares interpretable supervised models using different feature blocks, protocol branches and target definitions. The analysis focuses on internal validation, protocol-aware modelling, performance comparison and stability of results.

The objective is not to produce a clinically validated classifier, but to assess whether the available descriptors carry useful exploratory information for selected cardiometabolic outcomes.

#### `06_deep_learning.ipynb`

Contains exploratory deep-learning analyses based on waveform information.

This notebook evaluates whether raw or minimally processed TWE signals contain temporal information that may not be fully captured by handcrafted descriptors. It includes single-frequency waveform models, multi-frequency experiments and temporal convolutional network analyses.

Participant-level separation is preserved during evaluation. However, because different exploratory deep-learning configurations were compared using internal test-partition results, the reported performances are intended for exploratory model comparison and not as definitive independent validation.

## Data availability

The original biomedical dataset is not publicly available.

The data are excluded from this repository because they contain protected clinical and research information. Full reproduction of the analyses requires authorised access to the original dataset and the corresponding local configuration of input paths.

The repository is intended to document the analytical workflow without exposing confidential or protected information.

Where possible, the notebooks preserve the methodological structure of the workflow so that the code, decisions and analytical logic can be inspected and understood even when the protected dataset is not available.

## Reproducibility

The notebooks are provided for methodological transparency and code inspection.

Some parts of the workflow cannot be executed without access to the original protected dataset. Nevertheless, the repository documents the main analytical decisions, preprocessing steps, quality-control procedures, statistical analyses, modelling comparisons and evaluation principles used in the thesis.

The workflow is intended to be reproducible under equivalent authorised data-access conditions and with appropriate configuration of the original input paths.

## Repository status

This repository accompanies the final version of the Master's Thesis and is provided for methodological transparency and code inspection.

The notebook organisation reflects the analytical workflow described in the thesis. Protected biomedical data are not included, and full execution requires authorised access to the original dataset and local configuration of the corresponding input paths.

## Requirements

The project was developed in Python using a notebook-based workflow.

Core dependencies include:

```text
numpy
pandas
scipy
statsmodels
scikit-learn
matplotlib
tensorflow
jupyter
```

Additional dependencies may be required depending on the local notebook environment and the specific execution path used.

## How to use this repository

Clone the repository:

```bash
git clone https://github.com/antoniignasi/MetabolicElastography.git
cd MetabolicElastography
```

Open the notebook directory:

```bash
cd notebooks
```

Open the complete workflow:

```bash
jupyter notebook 00_full_analysis.ipynb
```

Alternatively, open each analytical block separately:

```bash
jupyter notebook 01_preprocessing.ipynb
jupyter notebook 02_descriptive_audit.ipynb
jupyter notebook 03_signal_quality_control.ipynb
jupyter notebook 04_statistical_analysis.ipynb
jupyter notebook 05_machine_learning.ipynb
jupyter notebook 06_deep_learning.ipynb
```

Full execution requires access to the protected dataset and the correct local configuration of the corresponding input paths.

## Methodological limitations

The project should be interpreted as an exploratory and methodological analysis.

Important limitations include:

- absence of public access to the original dataset;
- heterogeneous acquisition protocol branches;
- repeated measurements within participants and anatomical sites;
- possible protocol-induced structure in clustering and multivariate analyses;
- missingness and instability in some physical and viscosity-related variables;
- acquisition-level frequency-wise screening with potentially correlated repeated observations;
- limited effective sample size for some protocol-site-target combinations;
- exploratory internal validation only;
- use of internal test-partition results during deep-learning model comparison;
- absence of independent external or prospectively reserved final validation;
- exploratory nature of the predictive modelling results.

These limitations form part of the scientific interpretation of the work and are documented explicitly in order to avoid overstating the clinical meaning of the results.

## Main contribution

The main contribution of MetabolicElastography is not a final diagnostic model, but a transparent computational framework for analysing TWE data in a cardiometabolic setting.

The repository supports the thesis by documenting how raw signal files are transformed into structured analytical data, how mechanical and clinical variables are linked, how signal quality is evaluated, how protocol effects are considered, and how exploratory statistical and modelling analyses are interpreted under explicit methodological limitations.

## Author

Antoni Ignasi Cànaves Llabrés

Master's Thesis project  
Master's Degree in Bioinformatics and Biostatistics  
Universitat Oberta de Catalunya

## Disclaimer

This repository is intended for academic documentation and methodological transparency.

The code is shared for evaluation and research-documentation purposes. It does not include raw clinical data, identifiable information or protected research data.

The analyses presented here should not be interpreted as a validated clinical diagnostic system or as an independently validated predictive model.
