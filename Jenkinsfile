pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9' 
    }
    environment {
        DOCKER_HUB_USER = '3centennial1college3'
        IMAGE_NAME = 'jenkins-docker-maven-agile-lab3'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/lmananquilcentennialcollege/Jenkins-Web-App-Lab2.git'
            }
        }
        stage('Build Maven Project') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Docker Login') {  
            steps {
                withCredentials([string(credentialsId: 'dockerhub-credentials', variable:  'DOCKER_HUB_PASSWORD')]) {
                    bat "echo %DOCKER_HUB_PASSWORD% | docker login -u %DOCKER_HUB_USER% --password-stdin"
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t %DOCKER_HUB_USER%/%IMAGE_NAME% ."
            }
        }
        stage('Docker Push') {
            steps {
                bat "docker push %DOCKER_HUB_USER%/%IMAGE_NAME%"
            }
        }
        stage('Deploy') {
            steps {
                bat "docker run -d -p 9090:8080 %DOCKER_HUB_USER%/%IMAGE_NAME%"
            }
        }
    }
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
