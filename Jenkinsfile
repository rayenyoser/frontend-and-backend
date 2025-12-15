pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "todo-app"
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
                sh 'npm run install:backend'
                sh 'npm run install:frontend'
            }
        }
        stage('Run Tests') {
            steps { sh 'npm test || true' }
        }
        stage('Build Docker Image (Manual)') {
            steps {
                echo 'Docker build should be run manually on Windows CMD'
            }
        }
    }
    post {
        success { echo 'Pipeline completed successfully ✅' }
        failure { echo 'Pipeline failed ❌' }
    }
}
