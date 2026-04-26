# Student Performance Prediction — End-to-End ML Project

An end-to-end machine learning project that predicts student math scores based on demographic and academic features, with a Flask web app deployed on AWS Elastic Beanstalk.

## Overview

Given information about a student — their gender, ethnicity, parental education, lunch type, and test preparation — the model predicts their math exam score. Multiple regression models are benchmarked, with the best performer selected for the deployed web app.

## Dataset

**Students Performance in Exams** (UCI / Kaggle)

| Feature | Type | Description |
|---------|------|-------------|
| `gender` | Categorical | Male / Female |
| `race_ethnicity` | Categorical | Group A–E |
| `parental_level_of_education` | Categorical | Highest education level |
| `lunch` | Categorical | Standard / Free-reduced |
| `test_preparation_course` | Categorical | Completed / None |
| `reading_score` | Numeric | Reading exam score (0–100) |
| `writing_score` | Numeric | Writing exam score (0–100) |
| **`math_score`** | **Target** | **Math exam score (0–100)** |

## Models Benchmarked

| Model | R² Score |
|-------|----------|
| Linear Regression | — |
| Ridge | — |
| Lasso | — |
| K-Neighbors Regressor | — |
| Decision Tree | — |
| Random Forest | — |
| XGBRegressor | — |
| CatBoosting Regressor | — |
| AdaBoost Regressor | — |

*All models trained and evaluated; R² scores logged in `notebook/2. MODEL TRAINING.ipynb`.*

## Preprocessing

- **Numerical features**: StandardScaler
- **Categorical features**: OneHotEncoder
- Combined via `ColumnTransformer` into a single preprocessing pipeline

## Project Structure

```
Mproject/
    application.py          Flask entry point (AWS EB looks for this)
    notebook/
        1. EDA STUDENT PERFORMANCE.ipynb    Exploratory analysis
        2. MODEL TRAINING.ipynb             Model benchmarking & selection
        data/stud.csv                       Dataset
    src/
        components/         Data ingestion, transformation, model training
        pipeline/           Training and prediction pipelines
        exception.py        Custom exception handling
        logger.py           Logging setup
        utils.py            Shared utilities
    templates/
        index.html          Landing page
        home.html           Prediction form & results
    artifacts/              Generated model artifacts (after training)
    requirements.txt
    setup.py
    .ebextensions/          AWS Elastic Beanstalk config
```

## Setup

```bash
git clone https://github.com/Chirag-Mokashi/Mproject
cd Mproject
pip install -r requirements.txt
```

## Run Locally

```bash
python application.py
```

Open `http://localhost:5000`, fill in the student details form, and get a predicted math score.

## Training Pipeline

```bash
# Runs ingestion → transformation → model training → saves best model
python src/pipeline/train_pipeline.py
```

Or explore the notebooks in `notebook/` for the full EDA and model comparison.

## Deployment

Deployed on **AWS Elastic Beanstalk** — the entry point is `application.py` (EB convention).

```bash
eb init -p python-3.8 mproject
eb create mproject-env
eb deploy
```

## Tech Stack

- Python, Scikit-learn, XGBoost, CatBoost
- Pandas, NumPy, Matplotlib, Seaborn
- Flask (web interface)
- AWS Elastic Beanstalk (deployment)