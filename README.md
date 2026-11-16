# Multimodal Melanoma Classification Using Dermoscopic Images and Clinical Metadata

**Author:** Sarifa Siddika
Department of Computer Science and Engineering, Daffodil International University

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.24048285-blue)](https://doi.org/10.5281/zenodo.24048285)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-Streamlit-red)](https://skin-lesion-demo-sst.streamlit.app/)

## Links

- **Code and results (DOI):** https://doi.org/10.5281/zenodo.24048285
- **Live demo (Streamlit):** https://skin-lesion-demo-sst.streamlit.app/

## About

This project audits two established image-metadata fusion models for melanoma classification: feature concatenation (Fusion) and metadata-gated fusion (MetaBlock). Both use the same EfficientNet-B3 image encoder.

Instead of looking only at accuracy, the audit evaluates five things on the same trained models:

1. Discrimination (AUROC, accuracy, sensitivity, specificity)
2. Calibration (ECE, Brier score, log loss)
3. Modality dependence (zero-input ablation, image-only and metadata-only baselines)
4. Attribution agreement (Shapley values, Integrated Gradients and MetaBlock gate activation compared with ablation)
5. Robustness and sanity checks (randomization check, subgroups, alternative training run, gate interventions)

## Data

- **ISIC-DICM-17K** (primary): 15,097 dermoscopic images, six clinical variables. DOI: https://doi.org/10.34970/233480
- **PAD-UFES-20** (secondary): 2,298 smartphone images, cancer vs non-cancer. DOI: https://doi.org/10.1016/j.dib.2020.106221

Datasets are not redistributed here. Please download them from their original sources.

## What is in this repository

- Training, evaluation and attribution code
- Per-sample test predictions and per-run metrics for ISIC-DICM-17K and PAD-UFES-20

## Main findings

| Measure (ISIC-DICM-17K) | Fusion | MetaBlock |
|---|---|---|
| AUROC | 0.831 | 0.838 |
| Top-label ECE | 0.019 | 0.024 |
| Brier score | 0.168 | 0.165 |

- Image ablation reduced true-class probability about 4.4 times more than metadata ablation.
- Shapley agreement with ablation was high (rho = 0.992), but this is an internal consistency result.
- MetaBlock gate activation agreed weakly with ablation (rho = 0.212).
- Under an alternative training configuration, the AUROC difference disappeared.
- Prediction, calibration and attribution ranked the models differently, so they should be evaluated together.

All results are mean over five runs with group-aware (patient-level) splits.

## Live demo

Try the research demo here: https://skin-lesion-demo-sst.streamlit.app/

Upload a dermoscopic image, enter the clinical fields, and view the melanoma probability from both models with the attribution details.

## Important notice

This is a research project. The findings come from retrospective datasets without external clinical testing and **do not establish clinical utility**. The demo is **not a diagnostic tool** and must not be used for diagnosis or patient care.
