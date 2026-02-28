pipeline {
    agent any

    stages {

        stage('MAVEN Build') {
            steps {
                // Compile le projet
                sh 'mvn clean compile'
            }
        }

        stage('SONARQUBE') {
            environment {
                SONAR_HOST_URL = 'http://192.168.33.10:9000'
                SONAR_AUTH_TOKEN = credentials('sonarqube')
            }
            steps {
                sh """
                   mvn sonar:sonar \
                   -Dsonar.projectKey=devops_git \
                   -Dsonar.host.url=$SONAR_HOST_URL \
                   -Dsonar.login=$SONAR_AUTH_TOKEN
                """
            }
        }

    }
}
