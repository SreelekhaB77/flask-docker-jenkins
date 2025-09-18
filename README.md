Flask App CI/CD with Docker and Jenkins

This project demonstrates how to containerize a simple Flask application using Docker and automate its build and deployment with Jenkins.

🚀 Features

Flask backend application

Dockerized for easy deployment

Jenkins pipeline for CI/CD

Automatic builds triggered by GitHub Webhook

Runs on port 5000

📂 Project Structure
flask-docker-jenkins/
│── app/               # Flask app source code
│   └── app.py
│── Dockerfile         # Build instructions for Docker image
│── requirements.txt   # Python dependencies
│── Jenkinsfile        # CI/CD pipeline definition
│── README.md          # Project documentation

⚙️ Setup & Installation
1️⃣ Clone the Repository
git clone https://github.com/<your-username>/flask-docker-jenkins.git
cd flask-docker-jenkins

2️⃣ Build Docker Image
docker build -t flask-docker-jenkins .

3️⃣ Run Container
docker run -d -p 5000:5000 --name flask_app flask-docker-jenkins


Visit: http://localhost:5000

🔧 Jenkins Pipeline

The Jenkinsfile defines the stages:

Clone Repository
Pulls the latest code from GitHub.

Build Docker Image
Builds the Docker image using the Dockerfile.

Run Container
Removes old container (if exists) and starts a new one.

Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/<your-username>/flask-docker-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-docker-jenkins .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                  docker rm -f flask_app || true
                  docker run -d -p 5000:5000 --name flask_app flask-docker-jenkins
                '''
            }
        }
    }
}

🔔 GitHub Webhook Integration

In Jenkins job → Configure → Build Triggers

Select GitHub hook trigger for GITScm polling

In GitHub repo → Settings → Webhooks → Add Webhook

Payload URL:

http://<jenkins-server-ip>:8080/github-webhook/


Content type: application/json

Select: Just the push event

Now every git push will trigger Jenkins automatically 🚀.

🛠️ Requirements

Docker

Jenkins (with Git and Docker installed)

Python 3.x

✅ Future Improvements

Add unit tests in pipeline

Push Docker image to DockerHub

Deploy using Kubernetes or AWS ECS/EKS

