pipeline {
    agent any

    environment {
        // 'sonarqube' is the ID of your Jenkins credentials (token)
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
                // Inject SonarQube environment (URL, etc.)
                withSonarQubeEnv('SonarQube') {
                    // Pass the token explicitly to Maven
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
