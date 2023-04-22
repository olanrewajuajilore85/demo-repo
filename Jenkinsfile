pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
       // maven "mymaven"
        jdk "myjava"
    }

    stages {
        stage('Compile') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/olanrewajuajilore85/demo-repo.git'

                // Run Maven on a Unix agent.
                sh "mvn compile"

            }
        }

        stage('CodeReview') {
            steps{
                sh "mvn pmd:pmd"
            }
	    }
        stage('UnitTest') {
            steps{
                sh "mvn test"
			}
			post{
				always{
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
        stage('MetrixCheck') {
            steps{
                sh "mvn cobertura:cobertura -Dcobertura.report.format=xml"
			}
			post{
				always{
				    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
				}
			}
		}
				
        stage('Package'){
            steps{
                sh "mvn package"
        
            }
        }
    }
}
