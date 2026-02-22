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
              git branch: 'main',
                url: 'https://github.com/Tarakananda/New_Java_Project.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                export PATH=/opt/homebrew/bin:$PATH
                docker --version
                docker build -t tarakananda/employee-service:1.0 .
                '''
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

