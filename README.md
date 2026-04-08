# 🍷 Wine Quality Prediction — End-to-End MLOps Project with MLflow

An end-to-end machine learning project that predicts wine quality based on physicochemical properties. Built with a fully modular MLOps pipeline covering data ingestion to model deployment, with MLflow experiment tracking, Docker containerization, and CI/CD via GitHub Actions.

---

## 🔗 Tech Stack

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![MLflow](https://img.shields.io/badge/MLflow-Tracking-orange)
![Flask](https://img.shields.io/badge/Flask-Web%20App-lightgrey)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-green)
![AWS](https://img.shields.io/badge/Deployed-AWS%20EC2-yellow)

---

## 📌 Project Overview

This project demonstrates a production-ready ML workflow for predicting wine quality scores. The pipeline is fully modular — each stage (ingestion, validation, transformation, training, evaluation) is independently runnable and logged. The trained ElasticNet model is exposed via a Flask web app that allows real-time predictions.

---

## 🧱 Pipeline Architecture

Data Ingestion → Data Validation → Data Transformation → Model Training → Model Evaluation

Each stage is implemented as an independent pipeline class:

| Stage | File |
|-------|------|
| Data Ingestion | stage_01_data_ingestion.py |
| Data Validation | stage_02_data_validation.py |
| Data Transformation | stage_03_data_transformation.py |
| Model Training | stage_04_model_trainer.py |
| Model Evaluation | stage_05_model_evaluation.py |

---

## 📊 Model Details

- **Algorithm:** ElasticNet Regression (Scikit-learn)
- **Parameters (params.yaml):**
  - alpha: 0.4
  - l1_ratio: 0.3
- **Input Features (11):** fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol
- **Target:** Wine quality score

---

## 🧪 MLflow Experiment Tracking

All runs are tracked with MLflow — parameters, metrics, and model artifacts are logged automatically during the evaluation stage.

To view the MLflow UI locally, run:

    mlflow ui

Remote tracking is configured via DagsHub. Set the following environment variables before running:

    export MLFLOW_TRACKING_URI=https://dagshub.com/<your-username>/end-to-end-machine-learning-project-with-mlflow.mlflow
    export MLFLOW_TRACKING_USERNAME=<your-dagshub-username>
    export MLFLOW_TRACKING_PASSWORD=<your-dagshub-token>

---

## 🚀 Getting Started

### 1. Clone the repository

    git clone https://github.com/AdeebInamdar/end-to-end-machine-learning-project-with-mlflow.git
    cd end-to-end-machine-learning-project-with-mlflow

### 2. Create and activate a virtual environment

    python -m venv .venv
    source .venv/bin/activate        # Linux/Mac
    .venv\Scripts\activate           # Windows

### 3. Install dependencies

    pip install -r requirements.txt
    pip install -e .

### 4. Run the full training pipeline

    python main.py

### 5. Launch the Flask web app

    python app.py

Visit: http://localhost:8000

---

## 🌐 Web App Routes

| Route | Method | Description |
|-------|--------|-------------|
| / | GET | Home page |
| /train | GET | Trigger the full training pipeline |
| /predict | POST | Submit wine features and get quality prediction |

---

## 🐳 Docker

Build the image:

    docker build -t wine-quality-app .

Run the container:

    docker run -p 8000:8000 wine-quality-app

---

## ⚙️ CI/CD — GitHub Actions + AWS EC2

This project uses GitHub Actions for automated build and deployment:

1. On every push to main, the workflow builds a Docker image
2. The image is pushed to Amazon ECR
3. The container is pulled and deployed on an AWS EC2 instance

Required GitHub Secrets:

    AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY
    AWS_REGION
    AWS_ECR_LOGIN_URI
    ECR_REPOSITORY_NAME

---

## 📁 Project Structure

    ├── .github/workflows/       # CI/CD pipeline
    ├── config/                  # Configuration files
    ├── research/                # Jupyter notebooks (EDA & experiments)
    ├── src/mlProject/
    │   ├── pipeline/            # Stage-wise pipeline classes
    │   ├── components/          # Core ML components
    │   ├── config/              # Config manager
    │   ├── entity/              # Data classes
    │   └── utils/               # Helper utilities
    ├── static/                  # CSS/JS for web UI
    ├── templates/               # HTML templates (index, results)
    ├── app.py                   # Flask application
    ├── main.py                  # Pipeline entry point
    ├── params.yaml              # Model hyperparameters
    ├── schema.yaml              # Data schema for validation
    ├── Dockerfile               # Docker configuration
    ├── requirements.txt
    └── setup.py

---

## 👤 Author

**Adeeb M Inamdar**
- 📧 adeebinamdar2003@gmail.com
- 🔗 LinkedIn: https://linkedin.com/in/adeebinamdar
- 🐙 GitHub: https://github.com/adeebinamdar

---

## 📄 License

This project is licensed under the MIT License — see the LICENSE file for details.