// Declarative //
pipeline {
	agent any 
	stages {
		stage('Build') { 
			steps { 
				echo "Building"
				chmod +x wrapper.sh
				sudo docker build . -t sikariwal/hello:${BUILD_NUMBER}
				echo "Docker Image Built"
			}
		}
		stage('Push'){
			steps {
				echo "Pushing to Docker Hub"
				sudo docker login -u sikariwal -p ${DOCKER_HUB}
				sudo docker push sikariwal/hello:${BUILD_NUMBER}
				echo "Docker Image Pushed to Docker Hub"
			}
		}
		stage('Deploy') {
			steps {
				echo "Updating Deployment with New Image"
				kubectl set image deployment/hello hello=sikariwal/hello:${BUILD_NUMBER}
				echo "Updating Deployment with New Image"
			}
		}
	}
}
