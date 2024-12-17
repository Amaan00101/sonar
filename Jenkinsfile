pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        withSonarQubeEnv(installationName: 'sonarqube'){
          sh './mvnw clean install site surefire-report:report'
          sh 'tree'
        }
      }
    }
  }
}

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Amaan00101/sonar.git', credentialsId: 'git_credentials'
            }
        }

        stage('Build') {
            steps {
                // Use Maven directly
                sh 'mvn clean install site surefire-report:report'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=DevOps -Dsonar.host.url=http://localhost:9000/ -Dsonar.login=sonarqube-token'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}