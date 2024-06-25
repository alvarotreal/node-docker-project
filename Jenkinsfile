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
        
        stage ("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_ID', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                sh 'docker tag my-node-app:1.0 ajtreal/my-node-app:1.0'
                sh 'docker push ajtreal/my-node-app:1.0'
                sh 'docker logout'
               }          
            }        
        }

        stage ("Docker Run"){
            steps{
                sh 'docker run -p 87:3000 -d ajtreal/my-node-app:1.0'
            }
        } 

    }
} 
