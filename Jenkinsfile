pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('k8s') // Assuming you have stored your kubeconfig as a Jenkins credential
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository containing the Kubernetes manifests
                git branch: 'main', url: 'https://github.com/orestisthebeast/mod4-k8s.git'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Write the kubeconfig to a file
                    writeFile file: 'kubeconfig', text: KUBECONFIG
                    // Set the KUBECONFIG environment variable
                    withEnv(["KUBECONFIG=${pwd()}/kubeconfig"]) {
                        // Apply the Kubernetes manifest
                        sh 'kubectl apply -f task1.yaml'
                    }
                }
            }
        }
        stage('Verify Deployment') {
            steps {
                script {
                    // Verify that the deployment and service are running
                    withEnv(["KUBECONFIG=${pwd()}/kubeconfig"]) {
                        sh 'kubectl get deployments'
                        sh 'kubectl get svc'
                    }
                }
            }
        }
    }
    post {
        always {
            // Clean up the kubeconfig file
            deleteFile 'kubeconfig'
        }
    }
}
