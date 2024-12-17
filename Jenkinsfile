pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://localhost:9000'  // Replace with your SonarQube server URL
        SONARQUBE_TOKEN = credentials('sonarqube-token')  // Replace 'sonar-token' with your Jenkins credentials ID for the SonarQube token
    }

    stages {
        stage('Test SonarQube Connection') {
            steps {
                script {
                    // Run SonarQube Scanner to test connection
                    withSonarQubeEnv('sonarqube') {  // 'SonarQube' should match the name in Jenkins' SonarQube configuration
                        sh '''
                            sonar-scanner \
                              -Dsonar.host.url=$SONARQUBE_URL \
                              -Dsonar.login=$SONARQUBE_TOKEN
                        '''
                    }
                }
            }
        }
    }
}
