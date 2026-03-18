## 📌 Project Overview
This project is a Python-based application deployed using modern DevOps and cloud-native practices. It leverages containerization, Kubernetes orchestration, and CI/CD pipelines for scalable and automated deployment.

The application is structured using a modular architecture and is designed to run as a web service.

---

## 🔄 Basic Flow of the Project

1. **Application Initialization**
   - The application starts from `app.py`.
   - Environment variables are loaded using `dotenv`.
   - The app is created using a factory function (`create_app()`).

2. **Application Execution**
   - The app runs on host `0.0.0.0` and port `5000`.
   - Debug mode is enabled for development.

3. **Containerization**
   - The application is containerized using Docker.

4. **CI/CD Pipeline**
   - Code is pushed to GitHub.
   - CircleCI triggers a pipeline automatically.
   - The pipeline builds and pushes the Docker image to Artifact Registry.

5. **Deployment**
   - Kubernetes (GKE) pulls the image from Artifact Registry.
   - Deployment is managed via Kubernetes manifests.
   - Secrets (like API keys) are injected securely using Kubernetes secrets.

---

## 🛠️ Technologies Used

### 👨‍💻 Backend
- Python
- Flask (App Factory Pattern)

### ⚙️ DevOps & CI/CD
- Docker (Containerization)
- CircleCI (Continuous Integration & Deployment)
- GitHub (Version Control)

### ☁️ Cloud & Infrastructure
- Google Cloud Platform (GCP)
  - Google Kubernetes Engine (GKE)
  - Artifact Registry
  - Cloud Storage
  - IAM

### 🔐 Security & Configuration
- Environment Variables (`.env`)
- Kubernetes Secrets
- Base64 Encoding for secure key handling

---

## 🏗️ Project Architecture

            +-------------------+
            |   Developer       |
            |   (Code Push)     |
            +--------+----------+
                     |
                     v
            +-------------------+
            |     GitHub        |
            +--------+----------+
                     |
                     v
            +-------------------+
            |    CircleCI       |
            |  (CI/CD Pipeline) |
            +--------+----------+
                     |
      Build & Push Docker Image
                     |
                     v
      +----------------------------+
      |   Artifact Registry (GCP)  |
      +-------------+--------------+
                    |
                    v
      +----------------------------+
      |   GKE (Kubernetes Cluster) |
      |   - Deployment             |
      |   - Services               |
      +-------------+--------------+
                    |
                    v
            +-------------------+
            |   End Users       |
            +-------------------+

---

## 📄 Detailed Project Information

### 🔧 Application Entry Point
- `app.py` is the main entry point.
- It initializes the app and starts the server.

### ☁️ Cloud Setup
Before deployment, ensure:
- Required GCP APIs are enabled:
  - Kubernetes Engine API
  - Container Registry API
  - Compute Engine API
  - Cloud Build API
  - Cloud Storage API
  - IAM API

### 🧱 Infrastructure Setup
- Create a GKE Cluster.
- Create an Artifact Registry for storing Docker images.

### 🔐 Service Account Configuration
- A service account is created with roles like:
  - Storage Admin
  - Artifact Registry Admin
- Key is stored securely and encoded in Base64.

### 🔄 CI/CD Pipeline (CircleCI)
- Config file: `.circleci/config.yml`
- Environment variables required:
  - `GCLOUD_SERVICE_KEY`
  - `GOOGLE_PROJECT_ID`
  - `GKE_CLUSTER`
  - `GOOGLE_COMPUTE_REGION`

### 🔑 Secrets Management
- Kubernetes secrets are used to store sensitive data like API keys.
- Example: kubectl create secret generic llmops-secrets
           --from-literal=GROQ_API_KEY="your_actual_key"

### 🚀 Deployment Workflow
1. Developer pushes code.
2. CircleCI builds Docker image.
3. Image is pushed to Artifact Registry.
4. Kubernetes pulls and deploys the image.
5. Application becomes accessible to users.
