pipeline {
	agent any
	stages {
		stage ('GIT Clone') {
			steps {
				echo "Cloning the GIT Repository!"
				git 'https://github.com/Lakan-Ilaw/DevOpsClassCodes.git'
			}		
		}

		stage ('Compile') {
			steps {
				echo "Compiling the package!"
				sh 'mvn clean compile'
			}		
		}
		
		stage ('CMD Test') {
			steps {
				echo "PMD static code analysis initiated!"
				sh 'mvn pmd:pmd'
			}		
		}
		
		stage ('Unit Test') {
			parallel {
				stage ('Actual Unit Test') {
					steps {
						echo "Unit test initiated!"
						sh 'mvn test'
					}
					post {
						always {
							echo "The test has completed."
						}
						success {
							echo "The Unit Test is a success!"
						}
						failure {
							echo "It was a FAILURE!"
						}
					}
				}
				stepss ('STATUS') {
					steps {
						echo "TEST INITIANTED"
					}
				}
			}		
		}
		
		stage ('Build') {
			steps {
				echo "Building the package!"
				sh 'mvn package'
			}		
		}

		stage ('Validation') {
			steps {
				echo "Validation steps."
				sh 'mvn validate'
			}
		}

	}
}
