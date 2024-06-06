pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x
        GIT_EXECUTABLE = '/usr/bin/git'
    }
    stages {
        stage('Checkout') {
            steps {
                // Use the Git executable specified in the environment block
                script {
                    def gitCommand = sh(script: 'which git', returnStdout: true).trim()
                    if (gitCommand != env.GIT_EXECUTABLE) {
                        echo "Changing Git executable path to ${env.GIT_EXECUTABLE}"
                        env.PATH = "${env.GIT_EXECUTABLE}:${env.PATH}"
                    }
                }
                git branch: 'master', credentialsId: 'your-credentials-id', url: 'https://github.com/m-ayyaz/react-jenkins.git'
            }
        }
        // Add more stages as needed
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
