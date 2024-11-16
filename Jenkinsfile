pipeline {    
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('kuberaghu')
        IMAGE_NAME = "kuberaghu/dockerjenkins" 
    }
   
    stages {   
        stage('List Docker Images before Build') {
            steps {
                sh 'docker images'
            }
        }
      stage('Tag and Push Docker Images') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:Version${BUILD_NUMBER} .'
                sh 'docker push ${IMAGE_NAME}:Version${BUILD_NUMBER}'
            }
        }
     stage('List Docker Images after Build') {
            steps {
                sh 'docker images'
            }
        }
      stage('Remove Images after push') {
            steps {
                sh 'docker rmi ${IMAGE_NAME}:Version${BUILD_NUMBER}'
            }
        } 
    }
}
