pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "arunabi25/devops-website"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/arunkumarsenthilkumar25-dev/devops-practice.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop devops-container || true'
                sh 'docker rm devops-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 --name devops-container $DOCKER_IMAGE'
            }
        }

    }
}
