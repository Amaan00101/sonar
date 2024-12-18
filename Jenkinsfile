pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('soanrqube') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}