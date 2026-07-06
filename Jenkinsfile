pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				echo 'Building Phase'
				sh 'npm install'	
			}
		}
			
		stage('image building') {
			steps {
				echo 'Docker Image building'
				sh 'docker build -t samyakahire/devops-project:${BUILD_NUMBER} .'
			}
		}
		
		stage('image pushing') {
			steps {
				echo 'Docker image to image hub'
				sh 'docker push samyakahire/devops-project:${BUILD_NUMBER}'
			}
		}

		stage('k8s phase') {
			steps {
				echo 'Creating the deployment'
				sh 'kubectl apply -f project.yml'
			}
		}
	}	
}
