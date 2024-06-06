pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x'
    }

    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/m-ayyaz/react-jenkins.git'
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

    post {
        always {
            cleanWs()
        }
    }
}
