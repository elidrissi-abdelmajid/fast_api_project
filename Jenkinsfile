pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "mjid6/fast_api_image"
    }
    stages {
        stage('Clone Repository') {
           steps {
                    // Clone the GitHub repository
                    git branch: 'master', url: 'https://github.com/elidrissi-abdelmajid/fast_api_project.git'
                }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    bat  "docker build -t ${DOCKER_IMAGE}:latest ."
                }
            }
        }
    }
}
