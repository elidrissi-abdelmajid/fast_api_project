pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "mjid6/fast_api_image"
        DOCKER_TAG = "latest"
        REGISTRY_URL = "https://index.docker.io/v1/"
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
                    bat "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container to test if it works
                    bat "docker run -d -p 8000:8000 ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Log in to Docker Hub (Ensure you have credentials set up in Jenkins)
                    docker.withRegistry('', 'dockerhub-credentials') {
                        // Push the Docker image to Docker Hub
                        bat "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    }
                }
            }
        }
    }
    post {
        always {
            // Clean up any containers or images after the job is done
            bat "docker ps -a -q | xargs docker rm -f" // Remove all containers
            bat "docker images -q | xargs docker rmi -f" // Remove all images
        }
    }
}
