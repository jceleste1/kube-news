pipeline{
    agent any

	stages {
        stage('Build Dokcer Image') {
             steps{
                script { 
                    dockerapp = docker.build("jceleste/kube-news:v1", '-f ./src/Dockerfile ./src')
                }
            }
        }
    } 
}
