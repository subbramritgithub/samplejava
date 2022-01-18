pipeline {
    agent any
    stages {
        stage('compile') {
			steps {
                echo 'compiling..'
				git 'https://github.com/Tharak456/samplejava.git'
				bat label: '', script: 'mvn compile'
            }
        }
        stage('codereview-pmd') {
			steps {
                echo 'codereview..'
				bat label: '', script: 'mvn -P metrics pmd:pmd'
            }
        }
        stage('unit-test') {
			steps {
                echo 'codereview..'
				bat label: '', script: 'mvn test'
            }
			post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
			
        }
        stage('metric-check') {
			steps {
                echo 'unit test..'
				bat label: '', script: 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
			post {
                success {
				cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false                  
                }
            }
			
        }
        stage('package') {
			steps {
                echo 'metric-check..'
				bat label: '', script: 'mvn package'	
            }
			
        }
    }
}
