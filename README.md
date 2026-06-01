# Jenkins CI/CD Pipeline with Docker

## Project Overview

This project demonstrates a simple CI/CD pipeline using Jenkins and Docker. The pipeline automatically builds, tests, and deploys a Dockerized application whenever changes are pushed to the GitHub repository.

## Objective

Set up a basic Jenkins pipeline to automate the process of building and deploying an application.

## Tools Used

- Jenkins
- Docker
- GitHub
- Python (Sample Application)

## Project Structure

```text
jenkins-demo/
│
├── app.py
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## Application

### app.py

```python
print("Hello from Jenkins Pipeline")
```

## Docker Configuration

### Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY . .

CMD ["python", "app.py"]
```

## Jenkins Pipeline Stages

### 1. Checkout
Pulls the latest source code from GitHub.

### 2. Build
Builds the Docker image.

### 3. Test
Runs the Docker container and verifies the application.

### 4. Deploy
Deploys the application by running the Docker container.

## Jenkinsfile

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/sidraah/jenkins-demo.git'
            }
        }

        stage('Build') {
            steps {
                bat 'docker build -t jenkins-demo .'
            }
        }

        stage('Test') {
            steps {
                bat 'docker run --rm jenkins-demo'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker stop jenkins-demo-container || exit 0
                docker rm jenkins-demo-container || exit 0
                docker run -d --name jenkins-demo-container jenkins-demo
                '''
            }
        }
    }
}
```

## Setup Steps

1. Install Java JDK 17
2. Install Docker Desktop
3. Install Jenkins
4. Install Jenkins Plugins:
   - Git
   - GitHub
   - Docker
   - Docker Pipeline
   - Pipeline
5. Create GitHub Repository
6. Add project files
7. Configure Jenkins Pipeline Job
8. Connect GitHub Repository
9. Run Build
10. Verify Deployment

## Running the Project

Build Docker Image:

```bash
docker build -t jenkins-demo .
```

Run Container:

```bash
docker run --name jenkins-demo-container jenkins-demo
```

Check Running Containers:

```bash
docker ps
```

View Logs:

```bash
docker logs jenkins-demo-container
```

## Expected Output

```text
Hello from Jenkins Pipeline
```
##screenshots included
1. Jenkins Dashboard
2. Pipeline Job Configuration
3. GitHub Repository
4. Jenkinsfile
5. Successful Pipeline Stages
6. Docker Container Running


## Outcome

Successfully implemented a Jenkins CI/CD pipeline that automatically:
- Pulls source code from GitHub
- Builds a Docker image
- Tests the application
- Deploys the application using Docker
