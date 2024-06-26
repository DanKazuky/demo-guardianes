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
                junit '**/target/surefire-reports/*.xml'
            }
        }

        /*stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube_5') {
                    bat "${maven}/bin/mvn clean verify sonar:sonar " +
                                " -Dsonar.projectKey=PGSPOR-PORVENIRGUARD" +
                                ' -Dsonar.language=java' +
                                ' -Dsonar.java.binaries="."' +
                                ' -Dsonar.sourceEncoding=UTF8' +*/
        //                        " -Dsonar.exclusions=**/test/**/*.*" +
        /*                        ' -Dsonar.host.url=https://umanepre.emeal.nttdata.com/sonarqubece/' +
                                " -Dsonar.login=sqp_d3cbe9e7615d2bda861e3568310f752c02a9a88a"
                }
            }
        }*/
        stage('SonarQube Analysis') {
            tools {
               jdk 'JDK 11.0.1'
            }
            steps {
                withSonarQubeEnv('SonarQube_5') {
                  script {
                    bat "mvn sonar:sonar \
                        -Dsonar.projectKey=PGSPOR-PORVENIRGUARD \
                        -Dsonar.host.url=https://umanepre.emeal.nttdata.com/sonarqubece/ \
                        -Dsonar.login=sqp_d3cbe9e7615d2bda861e3568310f752c02a9a88a"
                    }
                }
            }
        }
    }
}
