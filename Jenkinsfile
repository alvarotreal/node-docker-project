pipeline {
    agent any

    tools {nodejs "nodejs"}
    
    stages {
        stage ('checkout') {
            steps{
                checkout scm
            }
        }

        stage ('Test') {
            steps{
                sh "npm install"
                sh "npm test"
            }
        }

        stage ('Build') {
            steps{
            sh 'npm run build'
            }
        }

        stage ('Build Image') {
            steps{
            sh 'docker build -t my-node-app:1.0 .'
            }
        }

        stage ('Push to DockerHub'){
            steps{
            withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerhub_id",usernameVariable:"dockerhubuser")]){
                sh "docker tag node-app-test-new ${env.dockerhubuser}/node-app-test-new:latest"
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhub_id}"
                sh "docker push ${env.dockerhubuser}/my-node-app:1.0"
                sh "docker logout"
            }
        }

    }
}
