pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git url: 'https://github.com/DanKazuky/demo-guardianes.git', branch: 'main', credentialsId: 'conexion-github'
            }
        }
 
        stage('Build') {
            steps {
                // Build commands
                sh '''
                echo "Building the project..."
                # comandos de build específicos del proyecto
                '''
            }
        }
 
        stage('Test') {
            steps {
                // Test commands
                sh '''
                echo "Running tests..."
                # comandos de test específicos del proyecto
                '''
            }
        }
    }
}
