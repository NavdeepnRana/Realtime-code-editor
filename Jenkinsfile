pipeline {
    agent any

    tools {
        maven 'Maven 3'
        jdk 'JDK 17'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Spring Backend') {
            steps {
                dir('backend-spring') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                bat 'npm install'
                bat 'set CI=false && npm run build'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    echo 'Building Docker images...'
                    bat 'docker-compose build'
                }
            }
        }
    }
}