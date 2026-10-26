
# SEER Lung Cancer Survival Prediction

A deep learning project that uses SEER cancer registry data to estimate time-dependent survival probabilities for patients diagnosed with lung and bronchus cancer.

## Overview

This project explores the application of neural networks to survival analysis using data from the Surveillance, Epidemiology, and End Results (SEER) Program. Unlike traditional classification models that predict a single outcome, survival analysis models estimate the probability of surviving beyond different time horizons while accounting for censored observations.

The objective is to develop a model that estimates survival probabilities based on patient demographics, tumor characteristics, diagnostic information, and other available clinical variables.

## Key Features

- **Survival analysis:** Models time-to-event outcomes while accounting for censored observations.
- **Neural network modeling:** Implements a discrete-time survival model using PyCox's Logistic-Hazard method.
- **Data preprocessing:** Handles missing values, encodes categorical variables, and transforms numerical features.
- **Exploratory data analysis:** Investigates feature distributions, data quality, and relationships between patient characteristics and survival.
- **Model evaluation:** Uses concordance and Brier score metrics to evaluate predictive performance.
- **Survival probability estimation:** Generates survival curves representing predicted survival probabilities over time.

## Dataset

The dataset was obtained through SEER*Stat from the Surveillance, Epidemiology, and End Results (SEER) Program and focuses on patients diagnosed with lung and bronchus cancer.

The data contains demographic, tumor-related, diagnostic, treatment, and survival information.

### Target Variables

- **Survival months:** Survival time, measured in months.
- **SEER cause-specific death classification:** The event indicator. Indicates whether a lung cancer-specific death was observed during the recorded follow-up period.

Patients who are alive or whose recorded death was attributed to another cause are treated as censored observations. Records with unknown or inapplicable cause-specific death classifications are excluded from the modeling dataset.

### Data Preprocessing

The preprocessing workflow includes:

- Examining missing values, unknown categories, and invalid measurements.
- Removing unsuitable or uninformative features.
- Encoding categorical variables and transforming numerical features.
- Handling missing numerical values using training-set-derived imputation statistics.
- Preparing duration and event labels for discrete-time survival modeling.

The original SEER data is not included in this repository. See the official [SEER Program](https://seer.cancer.gov/) for information about data access and use.

## Methodology

### Model Architecture

The project uses a neural network with PyCox's `LogisticHazard` method to model survival over discrete time intervals.

The model estimates conditional probabilities of experiencing the event across time intervals and combines these estimates to produce a survival function:

S(t | x) = P(T > t | X=x)

where \(T\) represents time to the event and \(x\) represents the patient's input features.

The resulting survival curve estimates the probability of surviving beyond each modeled time point.

### Training Workflow

1. Explore and preprocess the SEER dataset.
2. Split the data into training, validation, and test sets.
3. Fit preprocessing transformations and duration discretization using training data.
4. Train the neural network and monitor validation loss.
5. Apply early stopping to help limit overfitting.
6. Evaluate the final model on held-out test data.
7. Generate and analyze predicted survival curves.

## Evaluation

Model performance is assessed using survival analysis metrics.

| Metric | Purpose |
|---|---|
| Concordance index (C-index) | Measures how well the model ranks patients by survival risk. |
| Brier score | Measures the accuracy of predicted survival probabilities at specified time horizons. |

### Results

| Metric | Test Result |
|---|---|
| Concordance index | 0.8055 |
| Brier score | 0.06 -> 0.15 -> 0.04 |

The Brier score is evaluated across multiple time horizons to examine how the accuracy of survival probability estimates changes over time.

## Visualizations

The project includes visualizations to examine:

- Feature distributions and missing-data patterns.
- Relationships between patient characteristics and survival outcomes.
- Model training and validation performance.
- Predicted survival probability curves.
- Brier score performance across different time horizons.

![alt text](image.png)
<table>
  <tr>
    <td width="50%">
      <img src="image-1.png" width="100%" alt="Brier score over time">
      <p align="center"><em>Training & Validation Loss</em></p>
    </td>
    <td width="50%">
      <img src="image-2.png" width="100%" alt="Feature correlation heatmap">
      <p align="center"><em>Predicted Survival Curves</em></p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <img src="image-3.png" width="100%" alt="Survival time distribution">
      <p align="center"><em>Brier Score Over Time</em></p>
    </td>
  </tr>
</table>

## Technologies Used

- **Python**
- **Pandas and NumPy** — data manipulation and numerical computing
- **Scikit-learn** — preprocessing and data splitting
- **PyTorch** — neural network training
- **PyCox** — discrete-time survival modeling
- **Torchtuples** — neural network training utilities
- **Matplotlib and Seaborn** — data visualization
- **Jupyter Notebook** — experimentation and analysis

## Disclaimer

This project is intended for educational purposes. It is not a clinically validated prediction system and must not be used to make medical decisions.

## Data Attribution

Data source: [Surveillance, Epidemiology, and End Results (SEER) Program](https://seer.cancer.gov/).

Citation: Surveillance, Epidemiology, and End Results (SEER) Program (www.seer.cancer.gov) SEER*Stat Database: Incidence - SEER Research Data, 17 Registries, Nov 2023 Sub (2000-2021) - Linked To County Attributes - Time Dependent (1990-2022) Income/Rurality, 1969-2022 Counties, National Cancer Institute, DCCPS, Surveillance Research Program, released April 2024, based on the November 2023 submission.
