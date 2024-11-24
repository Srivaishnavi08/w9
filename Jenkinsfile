pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    // Build and push Docker image
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
                    // Explicitly set PATH
                    withEnv(['PATH=C:\\Program Files\\Kubernetes\\Minikube;C:\\Windows\\System32']) {
                        bat 'minikube version' // Verify Minikube is accessible
                        bat 'minikube delete || echo "No existing cluster to delete."'
                        bat 'minikube start'
                        bat 'minikube addons enable dashboard'
                        bat 'kubectl apply -f my-kube1-deployment.yaml'
                        bat 'kubectl apply -f my-kube1-service.yaml'
                        echo 'Deploying application...'
                    }
                }
            }
        }
    }
}
