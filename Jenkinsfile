pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_PROJECT_KEY = 'DevOps'
        SONAR_TOKEN = credentials('sonarqube-token') // Make sure the token is correct in Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out the repository"
                    // Checkout code from GitHub repository
                    git url: 'https://github.com/Amaan00101/sonar.git', branch: 'main' // Ensure correct branch
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    echo "Running Maven build and SonarQube scan"
                    withSonarQubeEnv('sonarqube') {  // Ensure SonarQube environment is correctly configured in Jenkins
                        sh '''
                        mvn -X clean verify sonar:sonar \
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
                echo "SonarQube scan complete. Check SonarQube dashboard for results."
                // Optional: Trigger additional actions like sending notifications
            }
        }
    }

    post {
        always {
            echo "Pipeline completed"
            // Cleanup or notification actions after the pipeline run
        }
    }
}
