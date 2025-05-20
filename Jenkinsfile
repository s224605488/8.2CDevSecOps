pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18'  // Replace with the name of NodeJS version you configured in Jenkins
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // matches the ID you added in Jenkins credentials
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {  // This should match the name in your Jenkins Sonar config
                    sh 'npx sonar-scanner'
                }
            }
        }
    }
}
