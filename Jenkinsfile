pipeline {
	agent {
		docker {
			image 'node:13.8'  
		}
	}
	stages {
		stage('Build') {
			steps {
				sh 'node --version'
				echo 'Build'
			}
		}
		stage('Test') {
			steps {
				echo 'Testing..'
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Testing..'
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
