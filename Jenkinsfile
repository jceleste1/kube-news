pipeline{
    agent any

	stages {
        stage('Build Dokcer Image') {
             steps{
                script { 
                    dockerapp = docker.build("jceleste/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
    } 

    stages {
         steps{
            script { 
                dockerapp = docker.withRegistry("https://registry.hub.docker.com", 'dockerhub')
                dockerapp.push('lastest')
                dockerapp.push("${env.BUILD_ID}")
            }
        }
    } 

}
