//declarative
pipeline {
	
	agent any

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Install'){
			steps {
				sh "mvn clean install"
			}
		}
		stage('Test'){
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Build Docker Image'){
			steps {
				//docker build -t jesusjrcardenas/currency-exchange-devops:$env.BUILD_TAG
				script {
					dockerImage = docker.build("jesusjrcardenas/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image'){
			steps {
				script {
					//dockerhub es la credencial creada previamente
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}	
				}
			}
		}

		stage('Package'){
			steps {
				// esto crea el jar
				sh "mvn package -DskipTests"
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

