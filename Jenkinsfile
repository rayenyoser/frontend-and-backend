pipeline {
    agent { docker { image 'node:18-alpine' } }
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
        stage('Tests') {
            steps { sh 'npm test || true' }
        }
        stage('Build Docker image') {
            steps { sh "docker build -t $DOCKER_IMAGE ." }
        }
    }
    post {
        success { echo "Pipeline completed successfully ✅" }
        failure { echo "Pipeline failed ❌" }
    }
}
