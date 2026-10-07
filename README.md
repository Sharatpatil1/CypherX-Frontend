# CypherX — Network Intrusion Detection System

CypherX is a complete NSL-KDD based binary network intrusion detection prototype. It classifies a connection as **Normal** or **Attack**, exposes the trained model through FastAPI, and provides a polished browser dashboard.

## Fastest way to run on Windows

1. Extract the ZIP.
2. Open the extracted `CypherX` folder.
3. Double-click **`START_CYPHERX.bat`**.
4. The script creates a virtual environment, installs dependencies, starts FastAPI and opens Chrome automatically.
5. Use **Traffic Detection → Load Normal / Load Attack → Classify traffic**.

Open manually: `http://127.0.0.1:8000`

**You do not need VS Code Live Server. The FastAPI server serves the frontend and API together.**

## API

- `GET /` — dashboard
- `GET /health` — server/model health
- `GET /model-info` — evaluation metrics and feature analysis
- `POST /predict` — 41-feature prediction endpoint
- `GET /docs` — Swagger API documentation

## ML pipeline

- Dataset: NSL-KDD
- Raw features: 41
- Candidate models: Logistic Regression, Decision Tree, Random Forest
- Selected model: Decision Tree (highest F1 in the generated evaluation)
- Preprocessor: numeric scaling + categorical one-hot encoding
- Live API output: binary **Normal / Attack**
- Attack category analysis: evaluated separately for Normal, DoS, Probe, R2L and U2R

## Included

- Frontend: HTML/CSS/JavaScript dashboard
- Backend: FastAPI + Pydantic
- Trained model and preprocessing artifacts
- NSL-KDD train/test data
- Training/preprocessing scripts
- Evaluation CSVs and charts
- Automated API/model tests

## Run tests

From the project folder:

```powershell
.\.venv\Scripts\python.exe -m pytest -q
```

Expected: all tests pass.

## Important demo note

The live inference endpoint is intentionally binary: **Normal vs Attack**. The dashboard's Analytics page contains category-level evaluation for DoS, Probe, R2L and U2R. Do not present the live endpoint as a multi-class attack-type predictor.


## Multi-connection detection
The Traffic Detection screen supports up to 10 complete NSL-KDD connection records at once. Use **+ Add connection**, **Duplicate current**, or **Load 5 Samples**, switch records using the numbered tabs, and use **Classify all** to send the complete queue to `POST /predict-batch`. Single-record `POST /predict` remains supported.
