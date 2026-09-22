cat > README.md <<'EOF'
# CI/CD Security Pipeline

An end-to-end CI/CD pipeline that automates source code checkout, static code analysis, Docker image creation, container image storage, and deployment.

## Architecture

GitHub → Jenkins → SonarQube → Docker → Nexus → Deployment

## Technologies Used

- GitHub
- Jenkins
- Jenkins Pipeline
- SonarQube
- Docker
- Nexus Repository
- Python
- Flask

## Pipeline Stages

### 1. Source Code Checkout

Jenkins retrieves the application source code from the GitHub repository.

### 2. Build

Jenkins executes the application build stage.

### 3. Static Code Analysis

SonarQube analyzes the Python application and Dockerfile for code quality and security-related issues.

### 4. Docker Image Build

Jenkins builds the application into a Docker image.

### 5. Nexus Repository

The Docker image is tagged and pushed to a Nexus Docker hosted repository.

### 6. Deployment

The Docker image is pulled from Nexus and deployed as a running container.

## Project Structure

```text
cicd-security-pipeline/
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
├── sonar-project.properties
├── jenkins/
│   └── Dockerfile
├── .gitignore
└── README.md
