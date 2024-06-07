pipeline {
    agent any

    tools {
        git 'Default'  // Ensure this matches the name in Global Tool Configuration
        nodejs 'Nodejs'   // Ensure 'Nodejs' is configured in Jenkins global tools
    }

    environment {
        NODE_VERSION = '22.x'
        DOCKER_IMAGE = 'mayyazmunir/react-jenkins'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsId: 'your-credentials-id', url: 'https://github.com/m-ayyaz/react-jenkins.git'
            }
        }

        stage('Install Node.js') {
            steps {
                script {
                    def nodejs = tool name: 'Nodejs', type: 'NodeJSInstallation'
                    env.PATH = "${nodejs}/bin:${env.PATH}"
                }
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
