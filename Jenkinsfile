pipeline {
    agent any

    // environment {
    //     SONARQUBE_SERVER = 'your-sonarqube-server' // Replace with your SonarQube server name
    //     SONARQUBE_CREDENTIALS = 'your-sonarqube-credentials-id' // Replace with your SonarQube credentials ID
    // }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your Git repository
                git url: 'https://github.com/Amaan00101/sonar.git', credentialsId: 'git_credentials'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Python dependencies
                sh 'pip install -r requirements.txt'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv(sonarqube) {
                    sh 'sonar-scanner -Dsonar.projectKey=DevOps -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000/ -Dsonar.login=sonarqube-token'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace or perform other actions
            cleanWs()
        }
    }
}