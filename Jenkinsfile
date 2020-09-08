//scripted
/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Test"
	}
}*/

//declarative
pipeline {
	agent any
	stages {
		stage('Build'){
			steps {
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
	} post {
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

