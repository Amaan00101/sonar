pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Amaan00101/training_day-11.git']])
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''mvn clean verify sonar:sonar -Dsonar.projectKey=DevOps -Dsonar
                    projectName='DevOps' -Dsonar.host.url=http://localhost:9000'''
                    echo 'SonarQube Analysis Completed'
                }

            }
        }
    }
}
