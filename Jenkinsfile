pipeline {    
    agent any 

    environment {
        registry = "kuberaghu/jenkinsdocker" 
        registryCredential = 'kuberaghu'
        
    }
   
    stages {   
       stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":V$BUILD_NUMBER" 
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
                script {
                    sh 'docker images'
                }
            }
        }
      stage('Remove Images after push') {
           steps {
                script{
                    sh "docker rmi $registry:V$BUILD_NUMBER" 
                }    
            }
        } 
    }
}
