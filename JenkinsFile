pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        DOCKER_IMAGE = "tarakananda/employee-service:1.0"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Tarakananda/New_Java_Project.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'PASS')]) {
                    sh 'docker login -u tarakananda -p $PASS'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
}

