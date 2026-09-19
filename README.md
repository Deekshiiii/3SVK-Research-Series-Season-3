# AirGuard AI — Hyperlocal Air Quality Prediction and Exposure Awareness

**Challenge contribution draft | 3SVK Research Series Season 3**

AirGuard AI is a reproducible machine-learning prototype that estimates short-term Air Quality Index (AQI) from pollutant, weather, and time features. It includes a transparent training pipeline, model comparison, a Streamlit interface, and batch CSV prediction.

> **Research integrity note:** The included CSV is synthetic demonstration data, not measured environmental observations. Metrics generated from it are software smoke-test results only and must not be reported as real-world model performance. Replace it with a permitted, documented real dataset before making empirical claims.

## Features
- Train and compare Random Forest and HistGradientBoosting regressors.
- Report MAE, RMSE, and R² on a held-out test split.
- Save the selected model and feature metadata.
- Predict AQI for a single observation or a batch CSV.
- Display a simple AQI interpretation guide.
- Keep data provenance and limitations explicit.

## Repository structure
```text
AirGuard_AI_Season3_Submission/
├── README.md
├── requirements.txt
├── research_paper.md
├── data/
│   ├── README.md
│   └── demo_synthetic_aqi.csv
└── src/
    ├── generate_demo_data.py
    ├── train_model.py
    └── app.py
```

## Setup
Use Python 3.10 or newer.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

## Run the demo
1. Generate or refresh the clearly labelled synthetic sample:
   ```bash
   python src/generate_demo_data.py
   ```
2. Train the models:
   ```bash
   python src/train_model.py --data data/demo_synthetic_aqi.csv
   ```
   The selected model and metrics are written to `artifacts/`.
3. Launch the app:
   ```bash
   streamlit run src/app.py
   ```

The app requires a trained model in `artifacts/`. Train first.

## Real-data workflow
1. Obtain a dataset that you are authorized to use, and record its source, license, geographical coverage, time period, and missing-value policy.
2. Convert it to CSV with the columns listed in `data/README.md`.
3. Train using `--data path/to/your_dataset.csv`.
4. Preserve the train/test split and report the evaluation results with the dataset provenance.
5. For time-series forecasting, use a chronological split rather than random splitting; the current script uses a random split and is intended as a baseline prototype.

## AQI interpretation
The category labels in the interface are broad user-facing guidance. AQI breakpoints differ by country and regulatory standard. This prototype does not claim to be an official public-health alert system.

## Team fields
Update the author/team fields in `research_paper.md` only after confirming the exact team details and consent to publish them.

## Limitations
- Synthetic demo data cannot establish environmental accuracy or public-health benefit.
- The current target is a supplied AQI value; it does not calculate regulatory AQI from pollutant sub-indices.
- A random split may leak temporal patterns; chronological validation is recommended for real deployment.
- The application is an educational research prototype, not medical advice or an official emergency-warning service.
