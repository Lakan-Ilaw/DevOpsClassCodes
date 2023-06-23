pipeline {
	agent any
	stages {
		stage ('GIT Clone') {
			step {
				echo "Cloning the GIT Repository!"
				git 'https://github.com/Lakan-Ilaw/DevOpsClassCodes.git'
			}		
		}

		stage ('Compile') {
			step {
				echo "Compiling the package!"
				sh 'mvn clean compile'
			}		
		}
		
		stage ('CMD Test') {
			step {
				echo "PMD static code analysis initiated!"
				sh 'mvn pmd:pmd'
			}		
		}
		
		stage ('Unit Test') {
			parallel {
				stage ('Actual Unit Test') {
					step {
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
				steps ('STATUS') {
					step {
						echo "TEST INITIANTED"
					}
				}
			}		
		}
		
		stage ('Build') {
			step {
				echo "Building the package!"
				sh 'mvn package'
			}		
		}

		stage ('Validation') {
			step {
				echo "Validation step."
				sh 'mvn validate'
			}
		}

	}
}
