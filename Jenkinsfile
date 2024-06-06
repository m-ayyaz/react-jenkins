pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x' // Make sure to close the string with a single quote
    }
    tools {
        git 'Default'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsI: 'key', url: 'https://github.com/m-ayyaz/react-jenkins.git'
            }
    }
        stage('Install Node.js') {
            steps {
                script {
                    // Use Node.js Plugin for Jenkins
                    tool name: 'Nodejs', type: 'NodeJSInstallation' // Correct the name of the Node.js installation
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
