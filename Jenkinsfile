pipeline {
    agent any
    tools {
        maven 'Maven 3.9.7'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git url: 'https://github.com/DanKazuky/demo-guardianes.git', branch: 'main', credentialsId: 'conexion-github'
            }
        }

        stage('Build') {
            steps {
                echo 'Build'
                bat "mvn --batch-mode package"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                bat "junit '**/target/surefire-reports/*.xml'"
            }
        }
    }
}
