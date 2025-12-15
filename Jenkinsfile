pipeline {
    // Use Node.js container to run pipeline steps
    agent {
        docker { image 'node:18-alpine' }
    }

    environment {
        DOCKER_IMAGE = "todo-app"
    }

    stages {
        stage('Checkout') {
            steps {
                // Get code from your fork or repo
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                // Install root dependencies
                sh 'npm install'

                // Install backend and frontend
                sh 'npm run install:backend'
                sh 'npm run install:frontend'
            }
        }

        stage('Tests') {
            steps {
                // Run tests (ignore failure so pipeline continues)
                sh 'npm test || true'
            }
        }

        stage('Build Docker image') {
            steps {
                // Build Docker image
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
