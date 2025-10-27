---
layout: default
title: Home
---

# MLOps Project Demo

A comprehensive MLOps project demonstrating data version control, experiment tracking, and CI/CD pipelines.

## Features

- 🔄 **Data Version Control**: Using DVC for tracking data changes
- 📊 **Experiment Tracking**: Using MLflow for tracking ML experiments
- 🚀 **CI/CD Pipelines**: Automated testing and deployment with GitHub Actions
- 🐳 **Containerization**: Docker support for reproducible environments
- 📚 **Documentation**: Comprehensive documentation and guides

## Quick Demo

### Data Version Control

```bash
# Initialize DVC
dvc init

# Track data files
dvc add data/iris_v1.csv
dvc add data/iris_v2.csv

# Check data changes
dvc diff
```

### Experiment Tracking

```bash
# Start MLflow UI
mlflow ui

# Run experiments
python ml/train.py --experiment-name iris_classification

# Compare experiments
mlflow ui
```

### Containerization

```bash
# Build Docker image
docker build -t ml-app .

# Run with Docker Compose
docker-compose up
```

## Project Architecture

```
ml-app-project/
├── app/           # Flask application
├── ml/            # Machine learning code
├── data/          # Data files
├── tests/         # Test files
├── .github/       # GitHub workflows
├── Dockerfile     # Docker configuration
└── docker-compose.yml  # Docker Compose configuration
```

## Getting Started

1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Initialize DVC: `dvc init`
4. Pull data: `dvc pull`
5. Run the application: `python app/main.py`

## Documentation

- [API Documentation](/api)
- [Demo Guide](/demo-guide)
- [MLOps Components](/mlops-components)