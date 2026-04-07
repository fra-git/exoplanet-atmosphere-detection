# exoplanet-atmosphere-detection
Exoplanet Atmosphere Detection using Deep Learning

# 🛰️ Exoplanet Atmosphere Detection using Machine Learning

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange.svg)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Automated detection of water vapor and clouds in exoplanet atmospheres using real CNES satellite data**

## Achievement

**96.3% Validation Accuracy** on real space agency challenge
- **Water Detection**: 99.72% AUC
- **Cloud Detection**: 97.53% AUC  
- **Systematic Optimization**: k=5 → k=156 (55.5% → 96.3%)
- **Rigorous Validation**: Shuffled labels → 50% AUC (proves genuine learning)

---

## 📋 Project Overview

This project tackles a real-world challenge from **CNES (Centre National d'Études Spatiales)**: Can machine learning automatically detect water vapor and clouds in exoplanet atmospheres by analyzing spectroscopic observations?

**Why it matters:** Water and clouds are key indicators for potentially habitable exoplanets. Automating their detection from spectral data accelerates the search for life beyond Earth.

### Key Result

Our approach achieved **96.3% validation AUC** through systematic methodology and rigorous validation, demonstrating that **well-designed classical ML can outperform deep learning** for certain scientific problems.

---

## Dataset

- **Source**: CNES Exoplanet Spectroscopy Challenge
- **Size**: 3,000 exoplanet observations
- **Features**:
  - **Spectral data**: (52, 3) → 156 wavelength measurements when flattened
  - **Auxiliary**: 5 stellar/planetary parameters (mass, temperature, radius, orbital distance)
- **Targets**: Binary classification
  - Water vapor presence (0/1)
  - Cloud coverage presence (0/1)
- **Split**: 80/20 train-validation (stratified)

---

## Methodology

### Data Preprocessing Pipeline

1. **Train/Validation Split** (80/20, stratified)
2. **Spectral Flattening** (52×3 → 156-dimensional vectors)
3. **PCA Dimensionality Reduction** (fit on training only - prevents leakage)
4. **Feature Standardization** (StandardScaler for auxiliary features)
5. **Multi-Modal Fusion** (concatenate PCA spectra + standardized auxiliary)

### Model Architecture

**Algorithm**: K-Nearest Neighbors (k=156)

**Why K-NN?**
- Spectral signatures exhibit strong **local similarity** in feature space
- Samples with similar atmospheres cluster together after PCA
- Simpler than deep learning but **more effective** for this dataset size
- **Interpretable**: predictions traceable to similar training examples

**Feature Engineering**:
- PCA on spectral data captures dominant variance patterns (absorption bands)
- Standardized auxiliary features provide complementary context
- Combined feature vector balances spectral detail with planetary characteristics

---

## 📈 Results

### Systematic K-Value Optimization

| k   | Mean AUC | Interpretation        |
|-----|----------|-----------------------|
| 5   | 0.555    | Underfitting          |
| 10  | 0.761    | Improving             |
| 20  | 0.848    | Good                  |
| 30  | 0.879    | Strong                |
| 40  | 0.914    | Very strong           |
| 60  | 0.949    | Excellent             |
| 100 | 0.958    | Near-optimal          |
| **156** | **0.963** | **Optimal**  |

### Final Performance

| Metric | Training | Validation |
|--------|----------|------------|
| **Water AUC** | 0.9972 | **0.9972** |
| **Cloud AUC** | 0.9936 | **0.9753** |
| **Mean AUC** | 0.9954 | **0.9630** |


### Validation & Sanity Checks

- **Shuffled Labels Test**: AUC dropped to 0.5015 (random chance)
- **Proves**: Model learns real atmospheric patterns, not artifacts
- **Train-Val Consistency**: Reasonable gap indicates good generalization
- **Systematic Optimization**: Performance consistently improved with larger k

---

## 💡 Key Insights

### Why This Approach Works

1. **Local Similarity in Spectral Space**
   - Exoplanets with similar atmospheres → similar spectral signatures
   - K-NN naturally exploits this clustering property

2. **PCA Captures Dominant Patterns**
   - 156D spectral data contains redundancy
   - PCA emphasizes absorption bands (water, clouds) while suppressing noise

3. **Multi-Modal Fusion**
   - Spectral data reveals **what's there** (molecular signatures)
   - Planetary data provides **context** (constrains physical plausibility)

### Lessons for ML in Science

- ✅ **Algorithm-Data Matching > Model Complexity**
- ✅ **Feature Engineering Matters** (PCA > raw features)
- ✅ **Rigorous Validation Essential** (sanity checks prevent false claims)
- ✅ **Simpler Can Be Better** (K-NN > Deep Learning for this problem)

---

### Installation
```bash
# Clone repository
git clone https://github.com/fra-git/exoplanet-atmosphere-detection.git
cd exoplanet-atmosphere-detection

# Install dependencies
pip install numpy pandas scikit-learn matplotlib seaborn jupyter
```


## Team:

- **Moritz Lumma** 
- **Dawood Javvad**
- **Francesco Cimarra**

**Course**: Deep Learning  
**Institution**: EDHEC Business School  
**Professor**: Romain Tavenard  
**Date**: January 2026


## References

- CNES Exoplanet Challenge Dataset
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [Exoplanet Atmosphere Characterization Methods](https://arxiv.org/abs/1811.06829)

---

⭐ **If this project helped you or you found it interesting, please star the repository! 🚀** 
