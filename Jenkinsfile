pipeline {
    agent any  // Runs on any available Jenkins agent

    tools {
        maven 'Maven 3.9.9'  // Use the Maven you configured in Jenkins
    }
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = 'jenkins-docker-maven-agile-maven-webapp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clones your GitHub repo
                git branch: 'main', url: 'https://github.com/lmananquilcentennialcollege/Jenkins-Web-App-Lab2.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build the Maven Web App
                bat 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests (if you have any)
                bat 'mvn test'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'docker login -u $DOCKER_HUB_CREDENTIALS_USR -p $DOCKER_HUB_CREDENTIALS_PSW'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }        

        stage('Deploy') {
            steps {
                // Simulate deployment (e.g., copying the .war file)
                echo 'Deploying the web app...'
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
