pipeline {    
    agent any 
   
    stages {   
        stage('List Docker Images before Build') {
            steps {
                sh 'docker images'
            }
        }
      stage('Tag and Push Docker Images') {
            steps {
                sh 'docker build -t ${ImageName}:${BUILD_NUMBER} .'
                sh 'docker push ${ImageName}:${BUILD_NUMBER}'
            }
        }
     stage('List Docker Images after Build') {
            steps {
                sh 'docker images'
            }
        }
      stage('Remove Images after push') {
            steps {
                sh 'docker rmi ${ImageName}:${BUILD_NUMBER}'
            }
        } 
    }
}
