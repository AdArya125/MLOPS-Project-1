# Vehicle Price Prediction - End-to-End MLOps Project

Welcome to the **Vehicle Price Prediction** MLOps project! This repository demonstrates a full-fledged Machine Learning workflow with seamless integration of:

- Automation
- Packaging
- Model Training
- Data Pipelines
- Cloud Integration
- Dockerization
- CI/CD with GitHub Actions & AWS

> **Goal**: Build a production-grade ML pipeline that predicts vehicle prices using modern DevOps principles.

---

## Project Architecture

```
                        +-------------------+
                        | Template Creation |
                        +--------+----------+
                                 ↓
                        +--------v----------+
                        | Environment Setup |
                        +--------+----------+
                                 ↓
                        +--------v----------+
                        | MongoDB Integration |
                        +--------+----------+
                                 ↓
        +------------------------v-------------------------------+
        | Data Pipelines (Ingestion, Validation, Transformation) |
        +------------------------+-------------------------------+
                                 ↓
            +--------------------v------------------------+
            | Model Training + Evaluation + Pushing to S3 |
            +--------------------+------------------------+
                                 ↓
              +------------------v------------------+
              | Flask API + Docker + EC2 Deployment |
              +-------------------------------------+
```

---

## Features

- Local package creation using `setup.py` and `pyproject.toml`
- MongoDB Atlas integration for scalable cloud-based storage
- Modular codebase with `src/` architecture and reusable configs
- Data ingestion, validation, transformation pipelines
- Model training, evaluation, and deployment logic
- AWS S3 model storage with versioning
- Real-time prediction API served with Flask
- CI/CD using Docker, GitHub Actions, ECR, and EC2
- Fully automated deployment on port `5080` with custom domain support

---

## Tech Stack

| Domain             | Tools / Services Used                     |
| ------------------ | ----------------------------------------- |
| Programming        | Python 3.10                               |
| Package Management | pip, conda                                |
| Data Storage       | MongoDB Atlas                             |
| Data Handling      | pandas, PyYAML                            |
| Model Training     | scikit-learn, custom estimators           |
| Cloud Services     | AWS S3, IAM, EC2, ECR                     |
| Deployment         | Flask, Docker, GitHub Actions             |
| CI/CD              | GitHub Actions, Self-hosted Runner on EC2 |

---

## Directory Structure

```
.
├── .github/workflows/
│   └── aws.yaml                # CI/CD workflow
├── src/
│   ├── components/             # Data ingestion, validation, transformation etc.
│   ├── configuration/          # MongoDB & AWS connections
│   ├── data_access/            # MongoDB data fetch logic
│   ├── entity/                 # Config and artifact entities
│   ├── aws_storage/            # AWS S3 integration
├── notebook/                   # EDA and MongoDB demo
├── templates/ & static/        # For Flask App
├── dockerfile                  # Docker setup
├── app.py                      # Flask application
├── requirements.txt
├── pyproject.toml & setup.py   # Local package management
└── README.md
```

---

## Setup Guide

### Create Project Template & Environment

```bash
python template.py
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
```

### Setup Local Packages

```bash
pip list  # Confirm local package installation
```

### MongoDB Atlas Integration

- Create project and cluster (M0 tier)
- Create DB user and whitelist `0.0.0.0/0`
- Copy the Python connection string (replace `<password>`)

### Setup Environment Variables

```bash
# Mac/Linux
export MONGODB_URL="mongodb+srv://<user>:<pass>@cluster.mongodb.net/..."

# Windows PowerShell
$env:MONGODB_URL = "mongodb+srv://<user>:<pass>@cluster.mongodb.net/..."
```

---

## ML Pipeline Components

### Data Ingestion

- Fetch raw data from MongoDB
- Convert to pandas DataFrame
- Store artifacts for next stage

### Data Validation

- Schema validation via `schema.yaml`
- Check for missing/null/incorrect data

### Data Transformation

- Feature engineering
- Convert raw features into model-ready format

### Model Training

- Custom training logic using `sklearn`
- Save best model artifact

### Model Evaluation & S3 Upload

- Compare old vs. new model
- Upload latest model to **AWS S3** if performance improves

---

## AWS Cloud Integration

### Setup AWS Credentials

```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
```

### S3 Bucket

- Region: `us-east-1`
- Bucket: `my-model-mlopsproj`

---

## CI/CD Pipeline with GitHub Actions & Docker

1. Configure `aws.yaml` under `.github/workflows`
2. Build Docker Image → Push to AWS ECR
3. Launch EC2 Instance → Connect EC2 to GitHub Runner
4. Auto-deploy Flask App to port `5000`

---

## Access the Application

Once deployed:

```text
http://<EC2-PUBLIC-IP>:5000/
```

Use `/training` route to manually trigger model training:

```text
http://<EC2-PUBLIC-IP>:5000/training
```

---

## Secrets Used in GitHub Actions

| Name                    | Description                    |
| ----------------------- | ------------------------------ |
| `AWS_ACCESS_KEY_ID`     | AWS Access Key                 |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Key                 |
| `AWS_DEFAULT_REGION`    | Default AWS Region (us-east-1) |
| `ECR_REPO`              | Docker Repo URI from AWS ECR   |

---

## Future Enhancements

- Add model drift detection
- Add monitoring with Prometheus/Grafana
- Integrate GitHub issues via bot
- Add frontend UI for better UX
- Switch to Terraform for infrastructure provisioning

---

## Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## License

This project is licensed under the MIT License.

---

## Author

**Aditya Arya**  
_Machine Learning Engineer | MLOps Enthusiast_

---

⭐ If you like this project, give it a star on GitHub!
