pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x'
    }
    tools {
        git 'Git'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsId: 'key', url: 'https://github.com/m-ayyaz/react-jenkins.git'
            }
        }
        stage('Install Node.js') {
            steps {
                script {
                    // Use Node.js Plugin for Jenkins
                    tool name: 'NodeJS 22', type: 'NodeJSInstallation'
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
    }
}
