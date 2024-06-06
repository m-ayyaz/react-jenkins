pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x'
        GIT_EXECUTABLE = '/usr/bin/git' // Change to the correct path of Git executable
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    def gitCommand = sh(script: 'which git', returnStdout: true).trim()
                    if (gitCommand != env.GIT_EXECUTABLE) {
                        echo "Changing Git executable path to ${env.GIT_EXECUTABLE}"
                        env.PATH = "${env.GIT_EXECUTABLE}:${env.PATH}"
                    }
                }
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
