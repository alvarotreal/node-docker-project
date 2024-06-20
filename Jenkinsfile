pipeline {
    agent any

    tools {NodeJS "NodeJS"}    
    stages {
        stage("checkout"){
            steps{
                checkout scm
            }
        }

        stage("Test"){
            steps{
                sh "npm install"
                sh "npm test"
            }
        }

        stage("Build"){
            steps{
            sh 'npm run build'
            }
        }
    }
}
