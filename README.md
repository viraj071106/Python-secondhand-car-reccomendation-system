# Second-hand car recommendation system

This project trains **Random Forest, Decision Tree, Ridge linear regression,
and KNN** models and combines them using weights learned from 5-fold
cross-validation on the training partition. The requested split is respected:
**30% of rows are used for training and 70% for testing**. The models use
imputation, one-hot encoding, scaling, regularization, depth limits, minimum
leaf sizes, and cross-validation to reduce both overfitting and underfitting.

## Run locally

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
# Put `used_cars_data.csv` in the project root
python train.py
uvicorn app:app --host 0.0.0.0 --port 8000
```

Open `http://127.0.0.1:8000/docs` for the interactive API. From a phone on
the same Wi-Fi, use `http://YOUR_LAPTOP_IP:8000/docs`; allow port 8000 through
the laptop firewall if needed. The service provides `/predict`, `/recommend`,
`/metrics`, `/metadata`, and `/health`.

Training writes `artifacts/model_bundle.joblib`, cleaned data, and
`artifacts/metrics.json`. It writes one actual-vs-predicted/residual plot per
model plus `reports/model_comparison.png`. Metrics include R², MAE, and RMSE;
for price regression, these are more meaningful than classification accuracy.

Example prediction body (replace keys using `/metadata`):

```json
{"features": {"year": 2018, "km_driven": 45000, "fuel": "Petrol", "transmission": "Manual"}}
```

Example recommendation body:

```json
{"budget": 800000, "preferences": {"fuel": "Petrol"}, "limit": 5}
```
