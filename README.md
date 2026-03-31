# 🥊 Boxing Audit Tool - SVR/SVM Round Scoring Analysis

[![R Version](https://img.shields.io/badge/R-4.0%2B-blue.svg)](https://www.r-project.org/)
[![Shiny](https://img.shields.io/badge/Shiny-1.7%2B-green.svg)](https://shiny.rstudio.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Development-orange.svg)]()

This project is a Senior Capstone Project for my B.A. degree program. An audit tool that uses Support Vector Machine (SVM) and Support Vector Regression (SVR) to analyze round-by-round scoring, predict the algorithm's verdict, and benchmarking with the judges' decisions.

# Table of Contents
- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [Model Architecture](#model-architecture)
- [Data Format](#data-format)
- [Results Interpretation](#results-interpretation)
- [Future Roadmap](#future-roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

# Overview

The Boxing Audit Tool is a sophisticated analytical platform designed to evaluate boxing match scoring using machine learning. It leverages Support Vector Machines (SVM) for classification tasks and Support Vector Regression (SVR) for continuous scoring prediction, providing a transparent, interpretable framework for analyzing boxing decisions.

# Why SVM/SVR for Boxing?
- Small Data Optimization: Perfect for the limited number of professional boxing matches
- Non-Linear Relationships: Captures complex interactions between boxing metrics
- Interpretability: Support vectors identify key rounds influencing decisions
- Regulatory Friendly: Transparent decision boundaries suitable for commission approval

# Features

# Core Functionality
- SVR Round Scoring: Predicts round-by-round scores (10-9, 10-8, etc.) based on fighter metrics
- SVM Agreement Analysis: Predicts whether automated scoring will match official judges
- Fight Summary Dashboard: Comprehensive overview of all analyzed fights
- Detailed Round Analysis: Break down of each round with confidence scores
- Model Comparison: Side-by-side SVR vs SVM performance metrics

# Visualization Capabilities
- Round score progression plots
- Support vector visualization (PCA projection)
- Confidence interval displays
- Agreement heatmaps
- Interactive data tables

# Audit Features
- Verdict comparison (SVR vs Official)
- Agreement tracking between models and judges
- Confidence scoring for each prediction
- Support vector identification and analysis

# Data Format
- Popular Matches.csv (kaggle dataset: link)
- Synthetic Round by Round Data.csv (link in the github)
## 🔧 How It Works

### Data Flow Architecture
