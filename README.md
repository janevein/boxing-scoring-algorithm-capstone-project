# 🥊 Boxing Audit Tool - SVM Verdict Classification

[![Python Version](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-red.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Deployed-brightgreen.svg)](https://boxing-scoring-audit-capstone-project-5kpdjajridrjqfa2ty6y.streamlit.app)

**Live Demo:** [Boxing Audit Tool on Streamlit Cloud](https://boxing-scoring-audit-capstone-project-5kpdjajridrjqfa2ty6y.streamlit.app)
To train the model, you can use the audit data in this github to see the demo.

This project is a Senior Capstone Project for my B.A. degree program. The Boxing Audit Tool uses Support Vector Machine (SVM) classification to predict boxing match verdicts based on fighter attribute differences. The tool provides an interactive web interface for uploading fight data, training the model, and exploring predictions through comprehensive visualizations.

## Table of Contents
- [Overview](#overview)
- [Live Demo](#live-demo)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Model Validation Approach](#model-validation-approach)
- [Installation](#installation)
- [Usage Guide](#usage-guide)
- [Data Format](#data-format)
- [Visualizations](#visualizations)
- [Model Performance](#model-performance)
- [Known Limitations](#known-limitations)
- [Technical Stack](#technical-stack)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Overview

The Boxing Audit Tool applies Support Vector Machine (SVM) classification to predict boxing match outcomes from fighter attribute differences. The system operates on three key differential features:

- **Power Difference**: Advantage in punching power (Fighter 1 - Fighter 2)
- **Resistance Difference**: Advantage in defensive capability
- **Ability Difference**: Advantage in chin durability (ability to take a punch)

By learning patterns from historical fight data, the SVM identifies the attribute signatures associated with different verdict types, currently supporting KO (Knockout), UD (Unanimous Decision), and SD (Split Decision) as the primary classes, with MD (Majority Decision) and RTD (Referee Technical Decision) available for datasets that include them.

## Live Demo

The application is permanently deployed on Streamlit Community Cloud:

**https://boxing-scoring-audit-capstone-project-5kpdjajridrjqfa2ty6y.streamlit.app**

The deployed version features a persistent URL, automatic HTTPS encryption, and global accessibility from any device with a web browser. No local installation is required.

## Key Features

### Core Functionality
- **SVM Multi-Class Classification**: Predicts verdict types based on three differential fighter attributes
- **Cross-Validation Performance Estimation**: 5-fold stratified cross-validation for robust accuracy reporting
- **Interactive Prediction Interface**: Real-time verdict prediction with adjustable attribute sliders
- **Support Vector Transparency**: Displays number of support vectors used by the model

### Visualization Capabilities
- **Confusion Matrix Heatmap**: Shows correct classifications and misclassification patterns
- **PCA Visualization**: 2D projection of the 3-dimensional feature space with explained variance ratios
- **Feature Distribution Box Plots**: Comparative analysis of attribute differences across verdict types
- **Probability Distribution Charts**: Visual representation of prediction confidence
- **Class Distribution Bar Charts**: Dataset composition analysis
- **Agreement Rate Charts**: Model performance by verdict type

### Validation & Transparency
- **5-Fold Stratified Cross-Validation**: Robust performance estimates with standard deviation
- **Training Accuracy Reference**: Provided for comparison (not to be confused with generalization)
- **Support Vector Count**: Indicates model complexity and potential memorization
- **Class Distribution Display**: Clear communication of dataset balance

## How It Works

### Data Processing Pipeline

When a user uploads a CSV file, the system performs the following preprocessing steps:

**1. Column Mapping**: Automatically detects and standardizes column names (e.g., `opponent_1_estimated_punch_power` → `opponent_1_power`)

**2. Round Aggregation**: If round-level data is present (indicated by a `round.x` column), aggregates to fight-level using mean values for each attribute

**3. Feature Engineering**: Computes differential features:
   - `power_diff` = Fighter 1 power - Fighter 2 power
   - `resistance_diff` = Fighter 1 resistance - Fighter 2 resistance
   - `ability_diff` = Fighter 1 ability to take punch - Fighter 2 ability

**4. Verdict Extraction**: Maps text verdict strings to standardized categories (KO, UD, SD, MD, RTD)

**5. Standardization**: Applies StandardScaler (z-score normalization: z = (x - μ) / σ) to ensure all features contribute equally to SVM optimization

### SVM Classification Architecture

The model uses the following configuration:
- **Kernel**: Radial Basis Function (RBF) - captures non-linear attribute interactions
- **Regularization (C)**: 10 - balances margin maximization against training error
- **Gamma**: 'scale' - automatically adapts kernel sensitivity (1/(n_features * X.var()))
- **Probability**: True - enables Platt scaling for well-calibrated confidence scores
- **Multi-class Strategy**: One-vs-One (OvO) via scikit-learn's SVC default

### Feature Processing Note

To avoid compatibility issues with different pandas/numpy versions on Streamlit Cloud, the code manually converts data from DataFrame rows to Python lists before creating numpy arrays:

```python
X_list = []
for idx, row in fight_data.iterrows():
    X_list.append([float(row['power_diff']), float(row['resistance_diff']), float(row['ability_diff'])])
X = np.array(X_list, dtype=np.float32)
