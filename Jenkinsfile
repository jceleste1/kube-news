pipeline{
    agent any

	stages {
        stage ('Build Dokcer Image'){
			script { 
				dockerapp = docker.build("jceleste/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
              }
        }
    } 
}
