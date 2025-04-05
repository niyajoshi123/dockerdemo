pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git 'https://github.com/niyajoshi123/dockerdemo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install dependencies (if needed for testing or linting)
                script {
                    sh 'pip install -r requirements.txt || true'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    sh 'docker build -t flask-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the Docker container
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-app-container flask-app'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker containers after the pipeline
            script {
                sh 'docker stop flask-app-container || true'
                sh 'docker rm flask-app-container || true'
            }
        }
    }
}