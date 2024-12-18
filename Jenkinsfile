pipeline{
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_PROJECT_KEY = 'DevOps'
        SONAR_TOKEN = credentials('sonarqube-token') // Store your SonarQube token in Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git 'https://github.com/Amaan00101/sonar.git'
            }
        }
        stage('Build and Test') {
            steps {
                script {
                    withSonarQubeEnv('sonarqube') {  
                        sh '''
                        mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                            -Dsonar.host.url=${SONAR_HOST_URL} \
                            -Dsonar.login=${SONAR_TOKEN}
                        '''
                    }
                }
            }
        }
    
        stage('Post-build Actions') {
            steps {
                script {
                    // Optional: Trigger additional actions like sending notifications
                    echo "SonarQube scan complete. Check SonarQube dashboard for results."
                }
            }
        }
    }
    post {
        always {
            // Cleanup or notification actions after the pipeline run
            echo "Pipeline completed"
        }
    }
}
