pipeline {
    agent any

    tools {
        maven 'Maven'   // must match Jenkins Maven tool name
        jdk 'JDK17'     // must match Jenkins JDK tool name
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

    }
}

