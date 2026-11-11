# Phase 1 — Fare and weather modeling

[Notebook](../../notebooks/phase-1-fare-and-weather-modeling.ipynb) · [Persian course report](../original/phase-1-course-report-fa.pdf) · [Data and setup](../../data/README.md)

## Objective and data

Phase 1 examines whether Uber and Lyft fares differ across service categories and how distance, surge pricing, and weather relate to fare prediction in the Boston sample. It also compares two classifiers for rain occurrence. The course extract contained 693,071 records across 12 zones, with 55,095 missing fares. Fare analyses used 637,976 records with a recorded price.

## Exploratory analysis

The team inspected missingness, reviewed origin–destination coverage, checked the mapping between service names and product identifiers, and used one-hot encoding for the service and company variables. Hourly and daily summaries describe time variation within the observation window. Histograms, quantile plots, normality tests, and interquartile-range summaries describe the distribution of prices.

A one-way analysis of variance (ANOVA) across service categories produced a saved F statistic of approximately 198,878. Tukey's honestly significant difference comparisons found a difference for all evaluated pairs except UberX and WAV at the specified 0.05 threshold. The group comparisons are descriptive because repeated records may share routes and time windows. The notebook applies a natural logarithm to fare and a square-root transformation to distance before the prediction exercises.

## Weather structure and rain classification

Principal component analysis (PCA) used standardized weather features. Eight components reached the 90% cumulative explained-variance threshold. The submitted K-means elbow analysis selected five clusters.

The rain classification target was positive precipitation intensity. The models excluded precipitation intensity and probability from their inputs and used a 70:30 stratified row split. The saved outputs are shown below.

| Classifier | Accuracy | Rain precision | Rain recall |
| --- | ---: | ---: | ---: |
| Logistic regression | 93.82% | 0.86 | 0.85 |
| Decision tree | 95.75% | 0.87 | 0.94 |

Nearby records can share weather conditions, so a row-based split can give optimistic performance for future dates. The accuracy figures describe this split.

## Fare prediction

The notebook compares correlation screening, recursive feature elimination, and least absolute shrinkage and selection operator (Lasso) feature selection. It fits two ordinary least squares (OLS) models, AdaBoost and XGBoost, and a stacking model with a ridge regression combiner. It also runs grid search and nine-configuration Taguchi trials. One submitted Taguchi cell is labeled AdaBoost but fits XGBoost. Its heading is corrected in the portfolio notebook.

| Model or feature set | Saved R² | Evaluation recorded by the notebook |
| --- | ---: | --- |
| OLS with correlation screening | 0.921 | Training fit |
| OLS with Lasso-selected predictors | 0.938 | Training fit |
| Baseline AdaBoost | 0.5725 | Training score |
| Baseline XGBoost | 0.9477 | Row-based holdout |
| Stacking ensemble | 0.9478 | Row-based holdout |

The stacking model recorded a root mean squared error (RMSE) of 0.1300 and a mean absolute error (MAE) of 0.0860 on the log-fare scale. The two OLS models recorded holdout RMSE values of 0.1591 and 0.1418, respectively, on that same scale.

These are saved course outputs. The fitting, feature selection, and tuning steps use different splits and samples, and some steps are unseeded. The scores therefore describe their respective evaluations and do not establish a single model ranking. The team favored the Lasso-selected OLS model when coefficient interpretation was the priority.

## Scope

The findings describe a short Boston dataset and the course's modeling choices. Temporal validation, a common evaluation protocol, and accuracy in the original fare units remain outside the submitted analysis.
