<h1 align="center">Causal Effect Variational Transformer<br>for Public Health Measures and COVID-19 Infection Cluster Analysis</h1>

<p align="center">
  <b>CIKM 2025</b><br>
  Jinho Kang, Sungjun Lim, Hojun Park, Jiyoung Jung, Jaehun Jung, Kyungwoo Song
</p>

<p align="center">
  <a href="https://dl.acm.org/doi/abs/10.1145/3746252.3761040"><img src="https://img.shields.io/badge/Paper-ACM%20DL-0085CA" alt="Paper"></a>
  <img src="https://img.shields.io/badge/CIKM-2025-8A2BE2" alt="CIKM 2025">
  <img src="https://img.shields.io/badge/python-3.10-3776AB?logo=python&logoColor=white" alt="Python 3.10">
  <img src="https://img.shields.io/badge/PyTorch-2.2-EE4C2C?logo=pytorch&logoColor=white" alt="PyTorch 2.2">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/6f753cc9-8288-4835-ae4f-9d31529f1463" width="90%" alt="Overall framework of CEVT">
</p>

Official PyTorch implementation of **CEVT**, a Transformer that estimates the causal effect of public health measures
on the spread of COVID-19 infection clusters.

- **Real-world data.** Two COVID-19 infection cluster datasets with public health measures, collected with local
  governments, a medical university, and a hospital, from two distinct distributions (provincial and municipal).
- **Cut-off augmentation.** Time series are sliced at different observation windows, which yields diverse
  feature–label pairs and mimics the partial observations of real settings.
- **Causal Effect Variational Transformer.** The model captures temporal structure and accounts for multiple
  treatments and latent confounders through an iterative conditioning mechanism.
- **Results.** CEVT outperforms the baselines in predicting confirmed cases and cluster durations, and its estimated
  causal effects agree with earlier findings on public health measures and infection spread.

## Overview

### Data

Clinical benchmarks with public health measures are scarce, so we collected time series of real infection clusters
together with the social distancing measures in force.

| Provincial COVID-19 data | Municipal COVID-19 data |
|:---:|:---:|
| <img src="https://github.com/user-attachments/assets/ae1a22f7-fc8c-4d34-aac5-bfd56baa0306" alt="Provincial COVID-19 data"> | <img src="https://github.com/user-attachments/assets/3981dff2-5786-42e4-9449-a866de12c3a4" alt="Municipal COVID-19 data"> |

The datasets are not released publicly. Access for non-commercial research can be requested (see
[`data/README.md`](data/README.md)).

### Cut-off augmentation

<p align="center">
  <img src="https://github.com/user-attachments/assets/5fccd5c4-2192-4dca-9aa9-f0031b61430f" width="80%" alt="Cut-off data augmentation">
</p>

### Model

<p align="center">
  <img src="https://github.com/user-attachments/assets/251e8b29-a490-4b40-bb57-4a783424cc20" width="80%" alt="Causal Effect Variational Transformer">
</p>

## Getting started

### Installation

Tested with Python 3.10.14.

```bash
pip install -r requirements.txt
```

Core packages: `pytorch 2.2.2`, `pandas 2.2.1`, `numpy 1.26.4`, `scikit-learn 1.4.1`, `scipy 1.11.4`.

### Running

```bash
bash sh/provincial_best.sh   # CEVT and the baselines on the provincial data
bash sh/municipal_best.sh    # CEVT and the baselines on the municipal data
```

### Code layout

```
├── data
│   ├── data_cut_0.csv ... data_cut_5.csv   # provincial data with cut-off augmentation
│   ├── data_final_mod.csv
│   ├── data_task.csv
│   └── municipal
│       └── preprocessed_municipal_98.csv   # municipal data
├── sh
│   ├── provincial_best.sh
│   └── municipal_best.sh
├── main.py               # CEVT and baselines
├── run_causal.py         # causal inference baselines (DragonNet, TARNet)
├── run_itransformer.py   # iTransformer baseline
├── models.py
└── utils.py
```

## Abstract

Recent research increasingly integrates causal inference into deep learning models to enhance the explainability and robustness of medical applications. However, data scarcity remains a fundamental challenge due to privacy constraints and the high cost of data collection. This issue, compounded by complex variable dependencies and unobserved latent confounders, hinders the reliable estimation of causal effects. To address these challenges, we collect two real-world COVID-19 infection cluster datasets, including public health measures, from distinct distributions in collaboration with local governments, a medical university, and a hospital. We also propose a cut-off augmentation method that generates diverse feature–label pairs by slicing time-series sequences at different observation windows, effectively simulating partial observations common in real-world settings. We further introduce the Causal Effect Variational Transformer (CEVT), a Transformer-based model that captures temporal structure while accounting for multiple treatments and latent confounders through an iterative conditioning mechanism. In real-world settings, CEVT outperforms baseline models in predicting confirmed cases and cluster durations, and provides more accurate estimates of the causal impacts of public health measures, demonstrating robust performance across datasets collected from distinct distributions. Moreover, the magnitude of causal effects estimated by CEVT is consistent with previous findings examining the relationship between public health measures and infection spread, further supporting the reliability of CEVT.

## Citation

```bibtex
@inproceedings{kang2025causal,
  title={Causal Effect Variational Transformer for Public Health Measures and COVID-19 Infection Cluster Analysis},
  author={Kang, Jinho and Lim, Sungjun and Park, Hojun and Jung, Jiyoung and Jung, Jaehun and Song, Kyungwoo},
  booktitle={Proceedings of the 34th ACM International Conference on Information and Knowledge Management},
  pages={1282--1291},
  year={2025}
}
```

The lab-maintained copy of this repository is at [MLAI-Yonsei/CEVT](https://github.com/MLAI-Yonsei/CEVT).
