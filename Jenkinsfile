pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'your-aws-region'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/m-ayyaz/react-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("mayyazmunir/react-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    sh 'aws eks update-kubeconfig --name react-app-cluster --region your-aws-region'
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}
