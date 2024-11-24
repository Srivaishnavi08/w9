pipeline {
    agent any

    environment {
        // Ensure the PATH is correctly set in the environment (replace with your paths if needed)
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;C:\\Program Files\\Kubernetes\\Minikube;${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Current PATH: ${env.PATH}"
                    
                    // Verify Docker and Minikube commands
                    bat 'docker version'
                    bat 'minikube version'
                    
                    // Build Docker image
                    bat 'docker build -t w9-dd-app:latest .'
                    bat 'docker tag w9-dd-app:latest vaishnavi517/w9-dh-app:latest'
                    bat 'docker push vaishnavi517/w9-dh-app:latest'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Verify Docker is running in Jenkins environment
                    bat 'docker info'
                    
                    // Check Minikube status
                    bat 'minikube status'

                    // Delete existing Minikube cluster and start a new one with Docker driver
                    bat 'minikube delete || echo "No existing cluster to delete."'
                    bat 'minikube start --driver=docker'

                    // Enable the Minikube dashboard addon
                    bat 'minikube addons enable dashboard'

                    // Apply Kubernetes resources
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'

                    // Open the Minikube dashboard
                    bat 'minikube dashboard'

                    echo 'Deploying application...'
                }
            }
        }
    }
}
