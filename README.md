## How Temporal Coverage and Reconstruction Shape Greenland Glacier Retreat Forecasting

This repository contains the experimental workflow for forecasting **one-month-ahead glacier retreat change next month** using the Dryad Greenland Glacier dataset. The study compares temporal data representations, context-window lengths, and model families including machine learning, deep learning, and pretrained foundation models.

## Overview

The workflow is organized into six stages:

1. **Data source** - Monthly observations for 226 Greenland glaciers from the Dryad Greenland Glacier dataset.
2. **Temporal representations** - Three ways of structuring glacier histories for modeling.
3. **Forecasting task** - Predict the next month’s retreat change.
4. **Model families** - Benchmark statistical, tree-based, deep-learning, and foundation-model approaches.
5. **Validation and testing** - Train, select configurations, and evaluate on held-out data using RMSE.
6. **Analysis** - Compare performance across data representations, context lengths, model stability, and fine-tuning strategies.

## Data

**Source:** Dryad Greenland Glacier dataset  
**Coverage:** 226 glaciers with monthly observations

The project uses three dataset representations:

| ID | Representation | Period | Glaciers | Description |
|---|---|---:|---:|---|
| D1 | As-is | 1992-2017 | 226 | Original heterogeneous glacier records with differing observation histories. |
| D2 | Common window | 2001-2010 | 226 | A controlled shared observation period for all glaciers. |
| D3 | Reconstructed | 1992-2017 | 204 | A reconstructed panel designed to provide more consistent longitudinal histories. |

## Forecasting Task

The target variable is:

```text
retreat_change_next_month
```

Each model predicts glacier retreat change for the following month using a trailing historical context window.

The evaluated context lengths are:

- 6 months
- 12 months
- 24 months
- 36 months

## Models

### Baseline

- Baseline benchmark model

### Statistical Models

- Linear Regression

### Tree-Based Machine Learning

- Random Forest
- XGBoost
- LightGBM

### Deep Learning

- Long Short-Term Memory (LSTM)
- Temporal Fusion Transformer (TFT)

### Foundation Models

Zero-shot pretrained models:

- Chronos 2
- Moirai

Fine-tuned models:

- Chronos 2
- Moirai

The experiments compare zero-shot performance with fine-tuned performance for the foundation models.

## Evaluation Workflow

For every combination of dataset representation, context length, and model configuration:

1. Train the model using the training set.
2. Validate candidate configurations and select the best context length and tuning setup.
3. Evaluate the selected configuration on the held-out test set.
4. Report **Root Mean Squared Error (RMSE)** as the primary metric.

Lower RMSE indicates more accurate one-month-ahead glacier retreat-change forecasts.

## Analysis Plan

The final analysis examines:

- Performance differences among D1, D2, and D3.
- Sensitivity to 6, 12, 24, and 36 month context windows.
- Model ranking and consistency across datasets and forecast contexts.
- Differences between zero-shot and fine-tuned foundation models.

## Reproducibility

For each experiment, record:

- Dataset representation (`D1`, `D2`, or `D3`)
- Train, validation, and test split definitions
- Context length
- Model name and hyperparameters
- Random seed
- Training hardware and software environment
- Test RMSE and any additional diagnostic metrics
