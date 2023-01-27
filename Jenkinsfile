pipeline{
    agent any

     def app

	stages {
        stage('Build Docker Image') {
             steps{
                script { 
                    app = docker.build("jceleste/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

         stage('Push Docker Image') {
            steps{
                script { 
                     app.withRegistry('https://registry.hub.docker.com', 'docker')
                    app.push('lastest')
                    app.push("${env.BUILD_ID}")
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
