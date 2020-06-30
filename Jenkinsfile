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
	stages {
		stage('Build') {
			steps {
				//sh 'mvn --version'
				//sh 'node --version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - #env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
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