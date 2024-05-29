pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git url: 'https://github.com/DanKazuky/demo-guardianes.git', branch: 'main', credentialsId: 'conexion-github'
            }
        }
    }
}
