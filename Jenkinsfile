pipeline {
    agent any

    environment {
        // Use the secret text credential ID for SonarQube token
        SONAR_AUTH_TOKEN = credentials('sonarqube')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling project...'
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                // Inject SonarQube URL and other env variables
                withSonarQubeEnv('SonarQube') {
                    // Pass the token explicitly
                    sh "mvn sonar:sonar -Dsonar.projectKey=devops_git -Dsonar.login=$SONAR_AUTH_TOKEN"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
