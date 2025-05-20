pipeline {
  agent any

  tools {
    nodejs 'NodeJS 18'
  }

  environment {
    SONAR_TOKEN = credentials('sonar-token') // Make sure this matches your Jenkins credential ID
  }

  stages {
    stage('Install') {
      steps {
        script {
          bat 'npm install'
        }
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
          bat 'npm audit'
        }
      }
    }
  }
}
