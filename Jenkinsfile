pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "mjid6/fast_api_image"
        DOCKER_TAG = "latest"
        DOCKER_PASS ="dckr_pat_knjjAjvRy6Qsy1arF36wVnB2Wug"
        KUBERNETES_CONFIG="k8s-deployment.yaml"
    }
    stages {
        stage('Clone Repository') {
            steps {
                //
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
        stage('login to docker hub ') {
            steps {
                script {
                    // Build the Docker image
                    bat "docker login -u mjid6 -p ${DOCKER_PASS}"
                }
            }
        }
        stage("test the docker image"){
            steps{
                script{
                    bat "docker images"
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                        bat "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                    
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply the Kubernetes configuration file
                    
                    bat "where kubectl "
                    bat "kubectl apply -f ${KUBERNETES_CONFIG} --validate=false --kubeconfig=C:\\Users\\USER\\.kube\\config"
                    bat "kubectl  get deployment --kubeconfig=C:\\Users\\USER\\.kube\\config"
                    // Optional: Print out the status of the deployment
                    bat "kubectl get services --kubeconfig=C:\\Users\\USER\\.kube\\config"
                    
                }
            }
        }
        stage('Verify Deployment') {
            steps {
                script {
                    // Wait for the deployment to be ready
                    bat "kubectl rollout status deployment/fast-api-deployment --kubeconfig=C:\\Users\\USER\\.kube\\config"
        
                    // Get the status of the services
                    bat "kubectl get svc --kubeconfig=C:\\Users\\USER\\.kube\\config"
        
                    // Optionally, you can use port-forward to test locally or check the logs for errors
                    bat "kubectl port-forward service/fast-api-service 8080:80 --kubeconfig=C:\\Users\\USER\\.kube\\config &"
                    bat "kubectl logs -l app=fast-api --kubeconfig=C:\\Users\\USER\\.kube\\config"
                }
            }
        }     
    }

}
