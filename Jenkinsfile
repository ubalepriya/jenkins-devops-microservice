//Declarative
pipeline {
	agent any
	/*agent {
		docker {
			image 'maven:3.6.3'
		}
	}*/
	stages {
		stage('Build') {
			steps {
				//sh 'mvn --version'
				echo "Build"
				echo "PATH : $PATH"
				echo "BUILD_ID : $env.BUILD_ID"
				echo "BUILD_NUMBER : $env.BUILD_NUMBER"
				echo "JOB_NAME : $env.JOB_NAME"
				echo "BUILD_TAG : $env.BUILD_TAG"
				echo "BUILD_URL : $env.BUILD_URL"
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
			echo 'I run always'
		}
		success {
					echo 'I run on success'
		}
		failure {
					echo 'I run on failure'
		}
		changed {
					echo 'I run when the build status changes'
		}
	}
}
