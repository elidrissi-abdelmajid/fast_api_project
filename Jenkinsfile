pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'b783918f-40e7-4124-b323-9b03167ad0bd', url: 'https://github.com/elidrissi-abdelmajid/fast_api_project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Ensure the docker command is available
                    def myImage = docker.build("my-image-name")
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        myImage.push('latest')
                    }
                }
            }
        }
    }
}


