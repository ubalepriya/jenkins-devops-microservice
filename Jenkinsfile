//Declarative
pipeline {
	agent any
	/*agent {
		docker {
			image 'maven:3.6.3'
		}
	}*/
	environment {
		mavenHome = tool 'myMaven'
		PATH	=	"$mavenHome/bin:$PATH"
	}
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
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
				sh "mvn clean compile" 
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
						dockerImage = docker.build("ubalepriya/currency-exchange-devops:${env.BUILD_TAG}") 
					  }
		}
		stage('Push Docker Image') {
					steps {
						script {
							//First parameter is to push to dockerHub, hence its empty
							docker.withRegistry('','myDockerHub'){
								dockerImage.push();
								dockerImage.push('latest');	
							}
						}
						
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
