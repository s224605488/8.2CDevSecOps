pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18' // Make sure this matches Jenkins NodeJS tool name
    }

    stages {
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    bat 'npm run sonar'
                }
            }
        }
        stage('Audit') {
            steps {
                bat 'npm audit'
            }
        }
    }
}
