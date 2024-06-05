pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-southeast-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/m-ayyaz/react-jenkins.git'
            }
        }


        stage('Deploy to EKS') {
            steps {
                script {
                    sh 'aws eks update-kubeconfig --name react-cluster --region ap-southeast-1'
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}
