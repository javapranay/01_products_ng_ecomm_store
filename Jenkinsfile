pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
               git branch: 'master', url: 'https://github.com/javapranay/01_products_ng_ecomm_store.git'
            }
        }
        
        stage('Docker Image Build'){
            steps{
                sh 'docker build -t javapranay/ecomm_store .'
            }
        }
        
       stage('Docker Image Push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u ashokit -p ${docker_pwd}'
                   sh 'docker push javapranay/ecomm_store'
            }
            }
        }
        
         stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }  
        
        
    }
}
