// Declarative //
pipeline {
	agent any 
	stages {
		stage('Build') {
		//	when {
		//		branch 'master'
		//	}
			steps { 
				echo "Building"
				sh "chmod +x wrapper.sh"
				sh "sudo docker build . -t sikariwal/hello:${BUILD_NUMBER}"
				echo "Docker Image Built"
			}
		}
		stage('Push'){
			steps {
				echo "Pushing to Docker Hub"
				sh "sudo docker login -u sikariwal -p ${DOCKER_HUB}"
				sh "sudo docker push sikariwal/hello:${BUILD_NUMBER}"
				echo "Docker Image Pushed to Docker Hub"
			}
		}
		stage('Deploy') {
			steps {
				echo "Updating Deployment with New Image"
				sh "kubectl set image deployment/hello hello=sikariwal/hello:${BUILD_NUMBER}"
				echo "Updating Deployment with New Image"
			}
		}
	}
}
