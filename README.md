# Multimodal Forecasting Framework for Predicting Earnings Surprises
**Grade:** 90.5 (Distinction)  
**Degree:** MSc Data Science & Artificial Intelligence – Queen Mary University of London  
**Author:** Stephanie Keddy  
**Supervisor:** Dr. William Marsh  
**Year:** 2025  

---

## Overview
This project introduces a **multimodal deep learning framework** for predicting **earnings surprises** in FTSE 100 companies.  
It integrates **financial language from earnings call transcripts** with **analyst consensus revision dynamics** to enhance forecasting of key performance metrics — *Revenue, EBITDA, EBIT, and Net Income.*

---

## Abstract
When year-end earnings results deviate from consensus forecasts, markets react.  
This study predicts the **magnitude of those surprises** using both textual and quantitative data, recalibrating forecasts by adding predicted surprises to existing analyst consensus values.  
A **rolling-origin design** ensures temporal realism and prevents look-ahead bias.  
Models were trained on FY2019–2023 and tested out-of-sample on FY2024.

**Results**
- Language-only model reduced mean absolute error (MAE) by **24.0%** for EBIT vs. baseline.  
- Hybrid (language + consensus dynamics) models achieved best overall reliability, improving EBITDA forecasts by **9.6%** and EBIT by **19.1%**.  
- All improvements for language and hybrid models across all forecast metrics were **statistically significant** (Diebold–Mariano test, *p* < 0.05).

---

## Framework
The pipeline combines:
- **Linguistic features** - structural, linguistic and lexicon-based features (Loughran-McDonald + own derived lexicons) 
- **FinBERT** – finance-specific sentiment analysis  
- **FinLLaMA** – financial-domain transformer embeddings (8k-token context)  
- **Consensus revision dynamics** – volatility, trend, and timing of analyst estimate changes  
- **Monte Carlo dropout ensembles** for uncertainty-aware forecasts  

**Workflow**
1. Parse HTML transcripts → structured tables (BeautifulSoup)  
2. Extract features → linguistic, sentiment, semantic embeddings  
3. Merge with consensus estimates and macroeconomic controls  
4. Train multimodal MLP ensemble models (PyTorch)  
5. Evaluate out-of-sample (FY2024)

---

## Tech Stack
- **Language Processing:** FinBERT, FinLLaMA, spaCy, Loughran-McDonald Lexicons + own derived lexicons  
- **ML Framework:** PyTorch, Scikit-learn  
- **Data Handling:** Pandas, NumPy  
- **Visualization:** Matplotlib, Seaborn  

---

## Key Results
| Metric | Best Model | Δ MAE vs Baseline | Win % | DM *p*-value |
|--------|-------------|-------------------|--------|---------------|
| Revenue | Language-only | −0.16% | 54.3% | 0.0000 |
| EBITDA | Hybrid | **−9.55%** | 56.0% | 0.0011 |
| EBIT | Language-only | **−24.0%** | 56.0% | 0.0000 |
| EBIT | Hybrid | **−19.1%** | **62.9%** | 0.0000 |
| Net Income | Hybrid | −3.17% | 66.0% | 0.0000 |

![EBITDA illustrative example](assets/Illustrative%20examples%20-%20EBITDA.png)

---

## Dissertation
The full dissertation (PDF) is available in the [`/reports`](reports/) folder:  
View --> [A Multimodal Framework for Predicting Surprises in Earnings Metrics of FTSE 100 Companies (PDF)](reports/S.Keddy%20-%20A%20Multimodal%20Framework%20for%20Predicting%20Surprises%20in%20Earnings%20Metrics%20of%20FTSE%20100%20Companies-FINAL.pdf)

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
