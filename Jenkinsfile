pipeline {
    agent any
    stages {
        stage("checkout"){
            steps{
                checkout scm
            }
        }

        stage("Test"){
            steps{
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage("Build"){
            sh 'npm run build'
        }
    }
}