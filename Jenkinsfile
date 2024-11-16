pipeline {    
    agent any 

    environment {
        registry = "kuberaghu/jenkinsdocker" 
        registryCredential = 'kuberaghu' 
        dockerImage = '' 
        
    }
   
    stages {   
        stage('List Docker Images before Build') {
            steps {
                sh 'sudo docker images'
            }
        }
       stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
      stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        }
     stage('List Docker Images after Build') {
            steps {
                sh 'sudo docker images'
            }
        }
      stage('Remove Images after push') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}
