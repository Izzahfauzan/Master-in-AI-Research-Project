# Predicting Performance Trajectories of Women Micro-Enterprises: An Early Warning Framework

This repository contains the research artefacts, machine-learning workflow, and prototype developed for my **Master of Artificial Intelligence research project at Universiti Malaya**.

The study explores how machine learning can be used to identify different business performance trajectories among women micro-entrepreneurs participating in **Ibupreneur Academy** and translate the predictions into an interpretable early-warning decision-support framework.

## Research Overview

Entrepreneurship support programmes often evaluate participant outcomes after a programme has ended. This research investigates whether information already collected through programme administration can be used earlier to identify participants who may require closer monitoring or additional support.

The study focuses on three business performance trajectories:

- **High**
- **Moderate**
- **Low / At-Risk**

The objective is not to automate programme decisions, but to provide administrators with additional evidence that can support human review and intervention planning.

## Research Objectives

This study aims to:

1. Examine how participant characteristics, business context, digital readiness, programme engagement and behaviour, and competency change contribute to the prediction of business performance trajectories.
2. Develop and compare interpretable machine-learning models for multiclass trajectory prediction.
3. Translate the selected model into an early-warning framework that can support participant monitoring and proactive intervention planning.

## Dataset

The original administrative dataset contained **201 participants** from seven Ibupreneur Academy cohorts conducted between 2025 and 2026.

After applying the analytical eligibility criteria, **173 participants** with complete longitudinal sales outcomes were retained for modelling.

The final trajectory distribution was:

| Trajectory | Participants | Percentage |
|---|---:|---:|
| High | 46 | 26.59% |
| Moderate | 84 | 48.55% |
| Low / At-Risk | 43 | 24.86% |

The primary modelling configuration used **18 predictors** covering:

- socio-demographic and business context
- business formalisation
- digital readiness
- programme engagement and behaviour
- competency change

> **Data Privacy:** Raw participant-level administrative data are not included in this public repository. Direct personal identifiers and confidential Ibupreneur Academy records are excluded to protect participant privacy.

## Methodology

The research follows the **CRISP-DM** framework:

1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modelling
5. Evaluation
6. Deployment

Three machine-learning algorithms were evaluated:

- Logistic Regression
- Random Forest
- XGBoost

Model performance was assessed using **nested stratified cross-validation**.

The primary model-selection metric was **Macro-F1**, supported by:

- Balanced Accuracy
- Macro Precision
- Macro Recall
- Multiclass ROC-AUC
- Low-class Recall
- Cross-validation stability

Preprocessing and model optimisation were performed within the cross-validation workflow to reduce the risk of data leakage.

## Model Performance

The primary model comparison produced the following results:

| Model | Macro-F1 | Balanced Accuracy | Macro ROC-AUC |
|---|---:|---:|---:|
| Logistic Regression | 0.371 | 0.375 | **0.588** |
| Random Forest | 0.366 | 0.366 | 0.583 |
| XGBoost | **0.403** | **0.405** | 0.565 |

**XGBoost** was selected as the final primary model because it achieved the strongest Macro-F1 and overall multiclass balance.

However, no single model performed best across every metric, and the results indicate that prediction remains challenging with the available administrative dataset.

## Explainable AI

To improve transparency, **SHAP (SHapley Additive exPlanations)** was applied to the selected XGBoost model.

SHAP was used for:

- global feature importance analysis
- participant-level prediction explanations
- identifying features contributing toward or away from the Low trajectory

The explanations represent how the fitted model uses the available predictors and **should not be interpreted as causal relationships**.

## Early-Warning Framework

The predicted probability of the Low trajectory was translated into three candidate monitoring bands:

- 🟢 **Green – Lower Risk**
- 🟠 **Amber – Monitor**
- 🔴 **Red – Administrative Review**

The candidate Amber and Red thresholds collectively identified **88.4% of participants who actually followed a Low trajectory**, while flagging **82.1% of the analytical sample**.

These thresholds are exploratory and require further prospective validation and recalibration before operational use.

## Prototype

An administrator-facing prototype was developed using **Gradio** and deployed through Hugging Face Spaces.

The prototype supports:

- individual participant assessment
- High, Moderate, and Low trajectory probabilities
- Low-class probability estimation
- Green, Amber, and Red monitoring bands
- SHAP-based explanations
- suggested administrative review areas
- cohort-level CSV screening

### Prototype

[Early Warning System – Hugging Face Space](https://huggingface.co/spaces/Izzzahfauzan/EarlyWarningSystem)

The prototype demonstrates technical feasibility and is intended as a **decision-support tool only**. It is not designed to automatically determine programme eligibility, funding, benefits, graduation, or access to assistance.

## Sensitivity Analysis

A separate sensitivity analysis examined the effect of including baseline financial variables:

- Sales Before Program
- Profit Before Program

Performance improved for several models when these variables were included. However, because baseline sales are structurally related to the trajectory definition, these variables were not used to replace the primary modelling configuration.

The sensitivity analysis was therefore treated as supporting evidence rather than the basis for final model selection.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- SHAP
- Matplotlib
- Gradio
- Hugging Face Spaces
- Jupyter Notebook / Google Colab

## Ethical Considerations

The research uses de-identified administrative data with organisational permission from Ibupreneur.

Participant-level predictions are intended to support human judgement rather than replace it. Contextual characteristics should not independently trigger punitive decisions, and no participant should be denied support or programme opportunities solely because of an automated risk score.

## Important Note

This repository is provided for **academic and research purposes**.

The model was developed using a relatively small administrative dataset from a specific entrepreneurship programme. The results should therefore not be interpreted as universally generalisable to all women micro-entrepreneurs.

Further research with larger datasets, additional cohorts, prospective validation, and threshold recalibration is required before the framework can be considered for operational deployment.

## Author

**Nur'Izzah Binti Fauzan**  
Master of Artificial Intelligence  
Universiti Malaya

Research Project:  
**Predicting Performance Trajectories of Women Micro-Enterprises: An Early Warning Framework**

## Acknowledgement

This research was conducted using administrative data from **Ibupreneur Academy**. I sincerely appreciate the organisation's support and permission for the academic use of the relevant de-identified programme data.

---

*This repository forms part of an academic research project submitted in fulfilment of the requirements of the Master of Artificial Intelligence programme at Universiti Malaya.*
