# AirGuard AI: A Reproducible Machine-Learning Prototype for AQI Estimation Using Pollutant and Meteorological Features

**Challenge:** 3SVK Research Series Season 3  
**Project type:** Applied machine-learning prototype  
**Authors/team:** [Enter confirmed participant names and team details]  
**Date:** [Enter submission date]

## Abstract
Air quality affects daily activities and environmental awareness, yet interpreting multiple pollutant and weather measurements can be difficult for non-specialist users. AirGuard AI is a reproducible prototype that estimates a numeric Air Quality Index (AQI) from pollutant concentrations, meteorological variables, and time features. The implementation compares Random Forest Regression with Histogram-based Gradient Boosting, evaluates models using mean absolute error (MAE), root mean squared error (RMSE), and coefficient of determination (R²), and exposes predictions through a Streamlit interface. A synthetic dataset is supplied only to verify that the software pipeline runs end-to-end. Since synthetic observations are not environmental measurements, no real-world accuracy or public-health effectiveness is claimed. Future evaluation requires documented, quality-controlled monitoring data and chronological validation.

**Keywords:** air quality, AQI estimation, machine learning, Random Forest, gradient boosting, environmental intelligence, reproducibility.

## 1. Problem statement
Air-quality information may be presented as multiple pollutant readings and weather measurements. A user-facing interface can help combine those inputs into a single model estimate, provided that the estimate is clearly distinguished from an official regulatory AQI calculation. This project investigates a compact supervised-learning workflow for AQI estimation and provides a reproducible prototype suitable for later evaluation on real observations.

## 2. Objectives
1. Build a consistent preprocessing and regression pipeline.
2. Compare two tree-based regression baselines.
3. Report MAE, RMSE, and R² on held-out observations.
4. Provide single-row and batch prediction interfaces.
5. document data provenance and limitations to prevent unsupported performance claims.

## 3. Input features and target
The model uses PM2.5, PM10, NO₂, SO₂, CO, O₃, temperature, relative humidity, wind speed, hour, and month as input features. The target is a numeric AQI value supplied by the dataset. This prototype does not calculate AQI from pollutant-specific regulatory sub-indices.

## 4. Methodology
### 4.1 Data preparation
The pipeline checks for required columns, converts infinite values to missing values, removes rows with a missing target, and imputes missing feature values using the training-set median through a scikit-learn pipeline.

### 4.2 Models
- **Random Forest Regressor:** an ensemble of decision trees trained on bootstrap samples.
- **HistGradientBoosting Regressor:** a boosting-based tree model that iteratively reduces residual error.

### 4.3 Evaluation
The current baseline uses a reproducible random train/test split. MAE measures average absolute prediction error, RMSE penalizes larger errors more strongly, and R² summarizes variance explained relative to a constant-mean baseline. The script selects the model with the lower test MAE. This random split is a preliminary baseline only; real temporal air-quality data should be evaluated with a chronological split and, where possible, station- or location-separated tests.

## 5. System architecture
1. **Data layer:** CSV observations and documented dataset metadata.
2. **Preprocessing layer:** required-column validation and median imputation.
3. **Learning layer:** Random Forest and HistGradientBoosting training.
4. **Evaluation layer:** MAE, RMSE, and R² calculation.
5. **Persistence layer:** serialized model and JSON metrics.
6. **Application layer:** Streamlit form for single-observation estimates and CSV batch prediction.

## 6. Implementation
The project is implemented in Python using pandas, NumPy, scikit-learn, joblib, Streamlit, and Plotly. `src/generate_demo_data.py` creates a simulated dataset; `src/train_model.py` trains and compares the regressors; and `src/app.py` serves the user interface.

## 7. Results and reporting policy
The included data is synthetic and generated from a simplified illustrative formula. Therefore, any metrics produced by running the demo describe only how well the selected regressors fit that artificial data-generation process. They are not evidence of performance on real air-quality measurements and are intentionally not presented here as empirical findings.

When a real dataset is used, report:
- dataset provider, version, license, geographic coverage, and date range;
- number of records and missing-data handling;
- exact train/validation/test strategy;
- MAE, RMSE, and R² for each model;
- any station-level or time-based generalization results;
- limitations and uncertainty.

## 8. Responsible-use considerations
Predictions can be affected by sensor calibration, missing measurements, location differences, changing weather, and distribution shifts. The prototype is not an official government AQI service, does not provide medical advice, and should not be used as the sole basis for health or emergency decisions. Regulatory thresholds and public-health guidance must be sourced from the relevant authority before any deployment.

## 9. Conclusion
AirGuard AI provides an end-to-end, reproducible baseline for learning-based AQI estimation, including model comparison, evaluation code, persistence, and a lightweight interface. The software is ready for demonstration with synthetic data. A valid environmental research conclusion requires training and testing on documented real observations, time-aware validation, and transparent reporting.

## 10. Future work
- Replace synthetic data with a licensed, quality-controlled dataset.
- Add chronological and location-held-out evaluation.
- Investigate forecasting horizons (for example, 1–24 hours) only when timestamped sequences and suitable labels are available.
- Add uncertainty intervals and drift monitoring.
- Compare predictions with official AQI definitions and clearly disclose any mismatch.
- Conduct usability and accessibility testing before deployment.

## References
1. Breiman, L. “Random Forests.” *Machine Learning*, 45, 5–32, 2001.
2. Friedman, J. H. “Greedy Function Approximation: A Gradient Boosting Machine.” *The Annals of Statistics*, 29(5), 1189–1232, 2001.
3. scikit-learn documentation, ensemble methods and model evaluation. Add the exact version/documentation URL used during final validation.
4. Add the real dataset citation, provider, version, and access date after selecting and verifying the dataset.

## Appendix A — Reproducibility
Install dependencies using `pip install -r requirements.txt`, generate the synthetic data using `python src/generate_demo_data.py`, train with `python src/train_model.py --data data/demo_synthetic_aqi.csv`, and launch the interface using `streamlit run src/app.py`.
