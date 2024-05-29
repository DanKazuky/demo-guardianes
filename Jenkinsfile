pipeline {

    agent any

    environment {
        BRANCH_NAME = "${env.gitlabSourceBranch}"
        GITURL = "${env.gitlabSourceRepoHttpUrl}"
		scannerHome = tool 'Sonar Scanner'
		projectKey = "PRODCO-COTECHLABSTEC"
		projectName = "CO-TechLabs-TechnicalDebt"
    }

    stages {

        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Build'
                sh "mvn --batch-mode package" 
            }
        }

        stage('Archive Unit Tests Results') {
            steps {
                echo 'Archive Unit Test Results'
               step([$class: 'JUnitResultArchiver', testResults: 'target/surefire-reports/TEST-*.xml'])
            }
        }
        
        stage('Publish Unit Test results report') {
            steps {
                echo 'Report'
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportDir: 'target/site/jacoco/', reportFiles: 'index.html', reportName: 'jacaco report', reportTitles: ''])

             }
        }
        
        stage('SonarQube Analysis') {
            tools {
               jdk 'JDK 11.0.1'
            }
            steps {
				withSonarQubeEnv('SonarQube 6 Community') {
					sh "${scannerHome}/bin/sonar-scanner" +
							' -Dsonar.language=java' +
							" -Dsonar.projectKey=${projectKey}" +
							" -Dsonar.projectName=${projectName}" +
							' -Dsonar.java.binaries="."' +
							" -Dsonar.projectVersion=${BUILD_NUMBER}" +
							' -Dsonar.sourceEncoding=UTF8' +
							" -Dsonar.exclusions=**/test/**/*.*"
				}
					
		    }
        }
    }
}


