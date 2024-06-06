pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x' // Make sure to close the string with a single quote
    }
    tools {
        git 'Default'
    }
    stages {
        stage('Test Git Access') {
            steps {
                script {
                    def gitVersion = sh(script: 'git --version', returnStdout: true).trim()
                    echo "Git version: ${gitVersion}"
                }
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsId: 'key', url: 'https://github.com/m-ayyaz/react-jenkins.git'
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
