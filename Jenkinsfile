pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
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
}

