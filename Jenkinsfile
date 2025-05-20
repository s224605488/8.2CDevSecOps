pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18'  // Must match Jenkins Tool Configuration name exactly
    }

    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'npm run sonar'
                }
            }
        }
        stage('Audit') {
            steps {
                sh 'npm audit'
            }
        }
    }
}
