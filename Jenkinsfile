//declarative
pipeline {
	
	agent {
		docker {
			image 'maven:3.6.3'
		}
	}

	stages {
		stage('Build'){
			steps {
				sh "mvn --version"
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
			}
		}
	}

	post {
		always {
			echo 'The pipeline has finished'
		}
		success {
			echo 'The pipeline has finished successfully'
		}
		failure {
			echo 'The pipeline has finished with a failure'
		}
	}
}

