pipeline {    
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('kuberaghu')
        IMAGE_NAME = "kuberaghu/dockerjenkins" 
    }
   
    stages {   
        stage('List Docker Images before Build') {
            steps {
                sh 'sudo docker images'
            }
        }
       stage('login to dockerhub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
      stage('Tag and Push Docker Images') {
            steps {
                sh 'sudo docker build -t ${IMAGE_NAME}:Version${BUILD_NUMBER} .'
                sh 'sudo docker push ${IMAGE_NAME}:Version${BUILD_NUMBER}'
            }
        }
     stage('List Docker Images after Build') {
            steps {
                sh 'sudo docker images'
            }
        }
      stage('Remove Images after push') {
            steps {
                sh 'sudo docker rmi ${IMAGE_NAME}:Version${BUILD_NUMBER}'
            }
        } 
    }
}
