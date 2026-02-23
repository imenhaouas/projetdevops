pipeline {
    agent any

    environment {
        SONAR_AUTH_TOKEN = credentials('sonarqube') // le token dans Jenkins Credentials
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
        withSonarQubeEnv('SonarQube') {
            sh 'mvn sonar:sonar -Dsonar.projectKey=devops_git'
        }
    }
}
    }
}
