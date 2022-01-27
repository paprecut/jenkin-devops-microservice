pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3' } }

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
			}
		}
		stage('Compile') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker image') {
			steps {
				//"docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG" this is the primitive way
				script {
					dockerImage = docker.build("docker build -t in28min/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker image') {
			steps {
				docker.withRegistry('', 'dockerhub') {
					dockerImage.push();
					dockerImage.push('latest');
				}
				
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