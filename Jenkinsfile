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
                    docker.build('fast-api-image')
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('fast-api-image').push('latest')
                    }
                }
            }
        }
    }
}
