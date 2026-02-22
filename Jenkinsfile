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
                withCredentials([usernamePassword(
                credentialsId: 'dockerhub-pass',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
                )]) {
            sh '''
            export PATH=/opt/homebrew/bin:$PATH
            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
            docker push tarakananda/employee-service:1.0
            '''
        }
    }
}



      }
    
    }

