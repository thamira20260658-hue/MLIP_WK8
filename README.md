# MLIP_WK8 — Model Deployment

End-to-end ML pipeline for the Week 8 (Model Deployment) exercise: train models on the
California Housing dataset, track experiments with MLflow, and serve the best model
through a FastAPI endpoint and a Streamlit UI.

## Project structure

```
config/        params.yaml — experiment name, seed, test size, model params
src/           data_loader.py, models.py, train.py, evaluate.py, utils.py
app/           api.py (FastAPI), streamlit_app.py (Streamlit)
doc/           assignment notes and architecture diagram
```

## Setup

```bash
conda activate <your-env>   # or create a venv
pip install -r requirements.txt
```

## Train

Run from the project root:

```bash
python -m src.train
```

This logs each model's params/metrics to MLflow and saves the best-performing model to
`models/best_model.pkl`.

View experiment runs:

```bash
mlflow ui
```

## Serve

FastAPI:

```bash
cd app
uvicorn api:app --reload --host 0.0.0.0 --port 8000
```

```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"features": {"MedInc": 5.0, "HouseAge": 20, "AveRooms": 5.0, "AveBedrms": 1.0, "Population": 800, "AveOccup": 3.0, "Latitude": 36.5, "Longitude": -119.0}}'
```

Streamlit:

```bash
cd app
streamlit run streamlit_app.py
```
