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
				withCredentials([usernamePassword(
					credentialsId: 'dockerhub'
					usernameVariable: 'DOCKER_USER',
					passwordVariable: 'DOCKER_PASS'
					)]) {		

					echo 'Docker image to image hub'
					sh '''
						echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin						
						docker push samyakahire/devops-project:${BUILD_NUMBER}
					'''
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
