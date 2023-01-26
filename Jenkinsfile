pipeline{
    agent any

	stages {
        stage ('Build Dokcer Image') {
			script { 
				dockerapp = docker.build("jceleste/kube-news:v1", '-f ./src/Dockerfile ./src')
              }
        }
    } 
}
