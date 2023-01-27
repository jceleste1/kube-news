pipeline{
    agent any

     environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }


	stages {
        stage('Build Docker Image') {
             steps{
                script { 
                    dockerapp = docker.build("jceleste/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

         stage('Push Docker Image') {
            steps{
                script { 
                    dockerapp = docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS)
                    dockerapp.push('lastest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        } 


      

        stage('Deploy Kubernetes') {
            steps{
               withKuberConfig([credentialsId: 'kubeconfig']){
                  sh 'sed -i "s/{{TAG}}/$tag_version/g" ./k8s/deployment.yaml'
                  sh 'kubectl apply -f ./k8s/deployment.yaml'
               }
            }
        } 


    }
}
