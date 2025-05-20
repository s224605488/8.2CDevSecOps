pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18'
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token')
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
        script {
            def auditStatus = bat(script: 'npm audit', returnStatus: true)
            if (auditStatus != 0) {
                echo "Audit found vulnerabilities. Continuing pipeline. Exit Code: ${auditStatus}"
            }
        }
    }
  }
}

