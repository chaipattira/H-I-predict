
# Leveraging Machine Learning for Predicting Galaxy HI Content

This project aims to develop a predictive model for the neutral hydrogen (HI) content of galaxies, leveraging machine learning techniques to approximate HI content more efficiently using commonly available galactic data, such as optical and morphological features. Direct HI measurement is time-intensive and limited to specific surveys; therefore, this model provides a scalable alternative for larger galaxy catalogs.

## Requirements

- Python 3.8+
- PyCaret
- Pandas, Numpy
- Matplotlib, Seaborn
- Scikit-Learn

Install the required libraries with:

```bash
pip install -r requirements.txt
```

## Repository Structure

```plaintext
.
├── input/                   # Dataset files (e.g., xGASS data)
├── figures/                # Figures for EDA and results
├── Report.tex              # Main LaTeX report file
├── README.md               # Project documentation
└── requirements.txt        # Python dependencies
└── main.ipynb               # Code files for data analysis and modeling
```

## Project Overview

### Motivation
HI content is essential for understanding a galaxy’s star formation potential and broader evolutionary patterns. This project automates a machine learning pipeline to predict HI content, specifically the logarithmic HI gas-to-stellar mass fraction (`lgGF`), using select features from the xGASS dataset.

### Key Features
The model uses six primary features:
1. **Magnitude-related properties:** 
   - `model_r`: r-band model magnitude
   - `NUVr`: NUV-to-r color index
2. **Morphological properties:** 
   - `expAB_r`: Axial ratio
   - `petrR50_r`: Radius enclosing 50% of Petrosian flux
   - `CINDX`: Concentration index
   - `INCL`: Inclination angle

### Methodology
The project employs the PyCaret library for streamlined model building, allowing for automated processing, comparison, tuning, and ensembling of machine learning models.

1. **Exploratory Data Analysis (EDA):** Relationships and trends within the selected features are analyzed to understand their interconnections and predictive power for `lgGF`. Key observations include the correlation of `NUVr` with `lgGF`, with bluer galaxies generally displaying a higher gas fraction.

2. **Baseline Model:** A multivariate linear regression model, with cross-validation, serves as the initial baseline, achieving an average \( R^2 \) of 0.768.

3. **Model Selection and Tuning:** PyCaret’s `compare_models()` identified CatBoost, Gradient Boosting Regressor, and Random Forest as top-performing models. These models were further optimized using grid search and blending to enhance prediction accuracy and generalization.

4. **Final Model and Results:** Ensembling CatBoost, GBR, and RF models resulted in an \( R^2 \) improvement from 0.809 to 0.895 and a notable reduction in hold-out sample error from 0.2953 to 0.2015. This blended model was finalized for practical deployment.

## Results

The final blended model outperforms individual models, capturing complex relationships in the data for more accurate HI content predictions.

### Key Findings:
- The NUV-to-r color index (`NUVr`) proved to be the dominant predictor, aligning with prior findings about galaxy color and gas content relationships.
- Blending and ensembling, facilitated by PyCaret, effectively stabilized model predictions, improving overall accuracy by ~12% over the baseline.

## Acknowledgments

This project was completed as part of a 12-hour hackathon at Columbia University. Special thanks to Blueshift and the organizers!
