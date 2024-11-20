pipeline {    
    agent any 

    environment {
        registry = "kuberaghu/jenkinsdocker" 
        registryCredential = 'kuberaghu' 
        dockerImage = '' 
        
    }
   
    stages {   
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
                        dockerImage.push(latest) 
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
                    // sh "docker rmi $registry:$BUILD_NUMBER" 
                }    
            }
        } 
    }
}
