**🚀 Flask + Docker + Jenkins CI/CD**

This project demonstrates how to deploy a Flask application inside a Docker container and automate the build & deployment using Jenkins Pipeline.

📂 **Project Structure**

flask-docker-jenkins/
│── app.py
│── requirements.txt
│── Dockerfile
│── Jenkinsfile
│── README.md


⚙️ **Setup & Run Locally**

 1️⃣ **Build Docker Image**
 
  docker build -t flask-docker-jenkins .

 2️⃣ **Run Container**
 
  docker run -d -p 5000:5000 --name flask_app flask-docker-jenkins

 3️⃣ **Test Application**

**Open in browser:**

http://localhost:5000


🔄 **Jenkins Pipeline**

The Jenkinsfile defines the stages:

Clone Repository → Pulls the latest code from GitHub

Build Docker Image → Builds the Docker image using the Dockerfile

Run Container → Removes old container (if exists) and starts a new one


📄 Jenkinsfile

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



