pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3.8.8'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/harikavelagala97/product-service.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t product-service:1.0 .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop product-service
                docker rm product-service
                docker run -d --name product-service -p 8082:8082 product-service:1.0
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline Finished'
        }
        success {
            echo 'Build Successful'
        }
        failure {
            echo 'Build Failed'
        }
    }
}