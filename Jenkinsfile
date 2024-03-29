pipeline {
	agent any
	environment {
		// Set the PATH variable to include JDK and Maven
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				echo 'Building..'
				echo "$PATH"
				echo "$env.BUILD_NUMBER"
				echo "$env.BUILD_ID"
				echo "$env.JOB_NAME"
				echo "$env.BUILD_TAG"
				echo "$env.BUILD_URL"
			}
		}
		stage('Complie') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				echo "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps {
				// sh "docker build -t naitikpatel/cur-exc-dev:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("naitikpatel/cur-exc-dev:0.0.0.1")
				}
			}
		}
		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	}

	post {
		always {
			echo 'This will always run'
		}
		success {
			echo 'This will run only if successful'
		}
		failure {
			echo 'This will run only if failed'
		}
		unstable {
			echo 'This will run only if the run was marked as unstable'
		}
		changed {
			echo 'This will run only if the state of the Pipeline has changed'
			echo 'For example, if the Pipeline was previously failing but is now successful'
		}
	}
}
