pipeline{
    agent any
        stages{
            stage("k8s"){
                steps{
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'mod4EKScluster', contextName: '', credentialsId: 'k8s', namespace: 'default', serverUrl: 'https://494DC0F033B24CB1F89C165EB78571E3.sk1.eu-west-2.eks.amazonaws.com']]) 
                    {
                    sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'
                    sh 'chmod u+x ./kubectl'
                    sh './kubectl get nodes'
                    sh './kubectl create -f pod.yaml'
                    sh './kubectl get pods'
                    }
                }    
        }
    }
}
