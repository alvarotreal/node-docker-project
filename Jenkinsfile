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
        
        stage("Push to Docker Hub"){
            steps{
            withDockerRegistry(credentialsId: 'DOCKERHUB_ID', toolName: 'docker') {
            sh 'docker push ajtreal:my-node-app:1.0'
            sh 'docker logout'
            
                }          
            }        
        }

    }
}
