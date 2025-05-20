pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SonarCloudToken') // Update with your Jenkins credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Tool Install') {
            steps {
                tool name: 'NodeJS 18', type: 'nodejs'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat 'npm install'
                }
            }
        }

        stage('SonarCloud Analysis') {
            environment {
                PATH = "${tool 'NodeJS 18'}\\bin;${env.PATH}"
            }
            steps {
                withSonarQubeEnv('SonarCloud') {
                    bat 'npx sonar-scanner'
                }
            }
        }

        stage('Audit') {
            steps {
                script {
                    bat(script: 'npm audit > audit-report.txt || exit 0')
                    archiveArtifacts artifacts: 'audit-report.txt', allowEmptyArchive: true
                }
            }
        }
    }
}
