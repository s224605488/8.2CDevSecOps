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
                    bat 'npx sonar-scanner'

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
