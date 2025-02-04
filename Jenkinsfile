pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('k8s')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/orestisthebeast/mod4-k8s.git'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    writeFile file: 'kubeconfig', text: KUBECONFIG
                    withEnv(["KUBECONFIG=${pwd()}/kubeconfig"]) {
                        sh 'kubectl apply -f task1.yaml'
                    }
                }
            }
        }
        stage('Verify Deployment') {
            steps {
                script {
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
            deleteFile 'kubeconfig'
        }
    }
}
