# A Multimodal Framework for Predicting Earnings Surprises in FTSE 100 Companies  

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)  
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep_Learning-red.svg)](https://pytorch.org/)  
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)  
[![MSc Distinction](https://img.shields.io/badge/Academic_Award-MSc_Distinction_90.5%25-brightgreen.svg)](#)

> **Stephanie Keddy — MSc Data Science & Artificial Intelligence, Queen Mary University of London**  
> *Supervised by Dr William Marsh*  

---

## 🧭 Overview  

Markets react sharply when companies deliver **earnings surprises** — deviations between reported and expected results.  
This project develops a **multimodal deep-learning framework** that anticipates these surprises *before disclosure*, by fusing:

- **Financial language** from *earnings-call transcripts*  
- **Quantitative consensus-revision dynamics** from *analyst forecast data*

> Achieved up to **24 % lower MAE** versus analyst baselines across FTSE 100 earnings forecasts by integrating **LLM-based financial NLP** with quantitative analyst dynamics.

The model forecasts **Revenue, EBITDA, EBIT, and Net Income** using a realistic **rolling-origin** setup to emulate pre-announcement prediction.

---

## 🎯 Objectives  

1. Predict continuous earnings-surprise magnitudes across multiple financial metrics.  
2. Integrate unstructured (language) and structured (consensus) data within one predictive framework.  
3. Recalibrate analyst forecasts to improve ex-ante accuracy.  
4. Evaluate reliability across post-disclosure horizons (+14 / +30 / +60 / +90 days).  

---

## ⚙️ Methodology  

### **Data Sources**  
| Source | Description |
|--------|-------------|
| MarketScreener | FTSE 100 earnings-call transcripts (2019 – 2024) |
| Bloomberg | Analyst consensus + actual financials |
| Bank of England / Yahoo Finance | Macro controls – base rate & FTSE 100 volatility |

> **Note:**  
> This repository does **not** include any raw or proprietary data.  
> All datasets referenced above were accessed through their respective platforms and remain subject to each source’s **terms of use and copyright policies**.  
> Users must obtain data directly from these providers if they wish to reproduce the results.

### **Feature Groups**  
- **Linguistic / Stylistic:** readability, tone, pronoun framing, complexity  
- **Sentiment:** FinBERT (finance-domain BERT classifier)  
- **Semantic Embeddings:** FinLLaMA (LLaMA-3-based 8k-token LLM)  
- **Consensus Dynamics:** revision volatility, timing, cross-metric trends  
- **Macroeconomic Controls:** interest rate & market volatility  

### **Model Architecture**  
- **Deep Ensemble MLPs (PyTorch)** — residual & compact variants  
- **Reference Models:** XGBoost · LightGBM (used to benchmark expected model performance during experimentation)  
- **Evaluation Baseline:** Unadjusted analyst consensus forecasts  
- **Techniques:** Monte Carlo Dropout · Adaptive Blending · One-Cycle LR · Variance-Inflation Screening  

---

## 📈 Key Results  

| Metric | Best Model | Δ MAE vs Baseline | Win % | DM *p*-value |
|--------|-------------|------------------|--------|---------------|
| Revenue | Language-only | −0.16% | 54.3% | 0.0000 |
| EBITDA | Hybrid | **−9.55%** | 56.0% | 0.0011 |
| EBIT | Language-only<br>Hybrid | **−24.0%**<br>**−19.1%** | 56.0%<br>**62.9%** | 0.0000 <br>0.0000 |
| Net Income | Hybrid | −3.17% | **66.0%** | 0.0000 |


📊 _Illustrative example (EBITDA prediction for CCEP):_  
![EBITDA Example](assets/Illustrative%20examples%20-%20EBITDA.png)

---

## 💡 Insights  

- **Both linguistic and consensus-dynamics features** provide systematic out-of-sample gains over the consensus baseline on FY2024 results, indicating complementary predictive value.  
- **Language-only models** (lexicon, FinBERT sentiment, FinLLaMA embeddings) often outperform structured inputs, achieving the largest MAE reduction for **EBIT (−24.0%)** and reliable gains for **Revenue**.  
- **Hybrid configurations** enhance robustness and case-level dominance (higher Win%), particularly for **EBITDA (−9.55% MAE)**, confirming that language and revision dynamics capture distinct, reinforcing information.  
- **Compact MLP architectures** generalize better and reduce overfitting, while **adaptive blending** stabilises deeper residual networks and improves Win% even when MAE gains are modest.  
- The framework establishes a **reproducible, time-aware approach** linking evolving analyst consensus with real corporate language, creating a scalable foundation for multimodal financial NLP and horizon-aware forecasting. 

---

### Notebooks
- [`EBITDA_model_training_evaluation.ipynb`](notebooks/EBITDA_model_training_evaluation.ipynb) — notebook covering model training, evaluation, and final testing for the *EBITDA* metric.  
  *Equivalent notebooks were developed for Revenue, EBIT, and Net Income during the MSc project; this version is representative of the full modelling approach.*
  
---

## 🧰 Tech Stack  

| Category | Tools |
|-----------|-------|
| **Language Processing** | Python 3.11 · BeautifulSoup 4 · spaCy 3.8 · textstat |
| **Financial NLP** | FinBERT · FinLLaMA |
| **Machine Learning** | PyTorch · scikit-learn · XGBoost · LightGBM |
| **Data & Visualisation** | pandas · NumPy · matplotlib · seaborn |
| **Statistical Testing** | Diebold–Mariano (Newey–West SE) |

---

## Dissertation
The full dissertation (PDF) is available in the [`/reports`](reports/) folder:  
View --> [A Multimodal Framework for Predicting Surprises in Earnings Metrics of FTSE 100 Companies (PDF)](reports/A%20Multimodal%20Framework%20for%20Predicting%20Surprises%20in%20Earnings%20Metrics%20of%20FTSE%20100%20Companies-UPLOAD.pdf)

---

## Author
**Stephanie Keddy**  
MSc Data Science & Artificial Intelligence (Distinction, GPA: 88.73 / 100)  
[LinkedIn](https://linkedin.com/in/steph-keddy)

---

## Citation
If referencing this work:
```bibtex
@mastersthesis{keddy2025multimodal,
  title={A Multimodal Framework for Predicting Surprises in Earnings Metrics of FTSE 100 Companies},
  author={Keddy, Stephanie},
  school={Queen Mary University of London},
  year={2025}
}
