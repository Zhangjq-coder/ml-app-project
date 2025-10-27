# ML App Project

This project demonstrates a machine learning application with DevOps and MLOps practices.

## Project Structure

```
.
├── app/                 # Application code
├── ml/                  # Machine learning components
│   ├── configs/         # Model configurations
│   └── registry/        # Model registry
├── data/                # Data directory (tracked by DVC)
├── tests/               # Test suite
├── .github/workflows/   # CI/CD pipelines
├── Dockerfile           # Docker configuration
├── requirements.txt     # Python dependencies
└── README.md           # This file
```

## Development Workflow

### Git Branching Strategy

- `main`: Production-ready code
- `staging`: Pre-production code
- `dev`: Development code
- `feature/*`: Feature branches

### CI/CD Pipeline

- On pull request to any protected branch:
  - Run test suite
  - Run linting/formatting/static analysis
  - Build Docker image
- On merge to staging:
  - Create staging environment
  - Build staging Docker image
- On merge to main:
  - Create production environment
  - Build production Docker image

## Getting Started

1. Clone the repository
2. Create a virtual environment: `python -m venv venv`
3. Activate the virtual environment:
   - Windows: `venv\Scripts\activate`
   - Unix: `source venv/bin/activate`
4. Install dependencies: `pip install -r requirements.txt`
5. Set up DVC: `dvc init`
6. Configure remote storage for DVC
7. Run the application: `python app/main.py`

## MLOps

### Data Versioning (DVC)

Data is versioned using DVC. Raw data is stored in Azure storage, with only .dvc pointer files tracked in Git.

### Experiment Tracking (MLflow)

ML experiments are tracked using MLflow. Each run logs:
- Code version (Git commit SHA)
- Dataset version (DVC dataset version)
- Hyperparameters
- Metrics
- Artifacts (models, plots)