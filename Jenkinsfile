pipeline {
    agent any

    stages {
        stage('MAVEN Build') {
            steps {
                // Compile the project
                // '-B' for non-interactive mode, '-DskipTests' to skip tests if desired
                sh 'mvn clean compile'
            }
        }

        stage('SONARQUBE') {
            environment {
                SONAR_HOST_URL = 'http://192.168.50.4:9000/' // Your SonarQube server URL
                SONAR_AUTH_TOKEN = credentials('sonarqube')  // Jenkins secret text ID
            }
            steps {
                // Run SonarQube analysis
                sh """
                   mvn sonar:sonar \
                       -Dsonar.projectKey=devops_git \
                       -Dsonar.host.url=$SONAR_HOST_URL \
                       -Dsonar.login=$SONAR_AUTH_TOKEN
                   """
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
