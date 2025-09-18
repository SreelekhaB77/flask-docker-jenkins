pipeline {
    agent any

    // Add this block to explicitly use the Git installation configured in Jenkins
    tools {
        git 'git version 2.43.0'  // <-- This must match the name in Manage Jenkins → Global Tool Configuration → Git
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone your repo using the specified Git tool
                git branch: 'main', url: 'https://github.com/SreelekhaB77/flask-docker-jenkins.git'
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

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
