# Next Cell State Analysis

A comprehensive single-cell RNA sequencing analysis pipeline for studying cell state transitions using CellRank and Palantir algorithms.

## Overview

This project analyzes single-cell RNA-seq data to understand cell state transitions and developmental trajectories. The analysis focuses on immature pyramidal neurons across different developmental timepoints (E16.5, P0, P5, P23) using advanced trajectory inference methods.

## Features

- **Comprehensive Preprocessing Pipeline**: Quality control, normalization, feature selection, and dimensionality reduction
- **Trajectory Inference**: Pseudotime analysis using Palantir algorithm
- **Cell State Prediction**: CellRank analysis for predicting cell fates and terminal states
- **Visualization**: UMAP embeddings and trajectory plots
- **Reproducible Environment**: Conda environment with all dependencies

## Dataset

The analysis uses the GSE104323 dataset, specifically focusing on:
- **Cell Type**: Immature pyramidal neurons
- **Time Points**: E16.5, P0, P5, P23 (embryonic to postnatal development)
- **Sample Size**: ~4,500 cells after quality control

## Installation

### Using Conda (Recommended)

```bash
# Create environment from the provided environment.yml
conda env create -f environment.yml

# Activate the environment
conda activate cellrank
```

### Using pip

```bash
# Install from requirements.txt
pip install -r requirements.txt
```

## Usage

### Basic Analysis

1. **Load and preprocess data**:
```python
import scanpy as sc
from notebooks.GSE104323_analysis import preprocess_time_series_data

# Load your data
adata = sc.read("path/to/your/data.h5ad")

# Preprocess
adata_processed = preprocess_time_series_data(
    adata, 
    time_col="development_stage", 
    celltype_col="cell_type"
)
```

2. **Run pseudotime analysis**:
```python
from notebooks.GSE104323_analysis import pseudotime

# Compute pseudotime
adata_with_pseudotime = pseudotime(adata_processed, early_cell='your_early_cell_id')
```

3. **CellRank analysis**:
```python
from notebooks.GSE104323_analysis import run_cellrank_analysis

# Run CellRank
results = run_cellrank_analysis(adata_with_pseudotime)
```

### Key Functions

- `preprocess_time_series_data()`: Comprehensive preprocessing pipeline
- `visualize_preprocessing()`: Diagnostic plots for quality control
- `pseudotime()`: Palantir-based pseudotime computation
- `run_cellrank_analysis()`: CellRank analysis with visualization

## Project Structure

```
next_cell_state/
├── notebooks/
│   └── GSE104323_analysis.ipynb    # Main analysis notebook
├── environment.yml                 # Conda environment specification
├── requirements.txt               # Python package requirements
└── README.md                      # This file
```

## Dependencies

### Core Libraries
- **scanpy**: Single-cell analysis in Python
- **cellrank**: Cell fate analysis
- **palantir**: Pseudotime inference
- **scvelo**: RNA velocity analysis
- **pandas**: Data manipulation
- **numpy**: Numerical computing
- **matplotlib**: Plotting
- **seaborn**: Statistical visualization

### Analysis Pipeline
1. **Quality Control**: Filter cells and genes based on standard metrics
2. **Normalization**: Log transformation and scaling
3. **Feature Selection**: Highly variable gene identification
4. **Dimensionality Reduction**: PCA and UMAP
5. **Clustering**: Leiden clustering
6. **Trajectory Analysis**: Palantir pseudotime computation
7. **Fate Prediction**: CellRank analysis for terminal states

## Results

The analysis produces:
- UMAP embeddings colored by time points, cell types, and clusters
- Pseudotime trajectories showing developmental progression
- CellRank fate probabilities and terminal state predictions
- Quality control metrics and diagnostic plots

## Citation

If you use this analysis pipeline, please cite the relevant papers:

- **CellRank**: Lange, M. et al. "CellRank for directed single-cell fate mapping." Nature Methods (2022)
- **Palantir**: Setty, M. et al. "Characterization of cell fate probabilities in single-cell data with Palantir." Nature Biotechnology (2019)
- **Scanpy**: Wolf, F.A. et al. "SCANPY: large-scale single-cell gene expression data analysis." Genome Biology (2018)

## License

This project is open source. Please check the individual package licenses for dependencies.

## Contact

For questions about this analysis, please open an issue in this repository.
