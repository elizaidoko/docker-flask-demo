pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('eliza-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                def docker = 'DockerHub'
                sh '$docker build -t ylmt/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                def docker = 'DockerHub'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                def docker = 'DockerHub'
                sh 'docker push ylmt/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            def docker = 'DockerHub'
            sh 'docker logout'
        }
    }
}
