pipeline {
	//agent any
	agent { 
		docker { 
			image 'node:16.13.1-alpine' 
			} 
		}
	stages {
		stage('Build') {
			steps {
				sh 'node --version'
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	post {
		always {
			echo 'I am awesome, I always run'
		}
		success {
			echo 'I run when you are successful 1'
		}
		failure {
			echo 'I run when you are fail'
		}
	}
}