pipeline {
    agent { label 'Slave-1'}

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
                withCredentials([string(credentialsId: 'Docker-token', variable: 'secretPass')]) {
                    sh 'docker login -u javapranay -p ${secretPass}'
                    sh 'docker push javapranay/ecomm_store'
                }
            }
        }
        
        /*stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }*/  
        // Deployment has to be done in CD job. So we have to create frontend cd job seperately which has to run on the Jenkins master only.
        
    }
}
