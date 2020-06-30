//Scripted pipeline approach
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

//Declarative pipeline approach
pipeline {
	agent any
	//agent { docker { image 'node:13.8' } }
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
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				//sh "docker build -t adamedens/currency-exchange-devops:$env.BUILD_TAG"
				script {
				 	def dockerImage = docker.build("adamedens/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest')
					}
				}
			}
		}
	}
	post {
		always {
			echo 'Always run after pipeline'
		}
		success {
			echo 'Only run when successful'
		}
		failure {
			echo 'Only run when pipeline fails'
		}
	}
}