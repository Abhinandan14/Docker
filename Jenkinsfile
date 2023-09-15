pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Abhinandan14/Docker.git']])
                sh 'mvn clean install'
            }
        }
    
        stage('Build docker image'){
            steps{
                
                script{
                    sh 'docker build -t abhinandan7/jenkins-task:latest .'
                }
            }
        }
        
        stage('Push image to Docker Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-newpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u abhinandan7 -p ${dockerhubpwd}'
}
                    sh 'docker push abhinandan7/jenkins-task:latest'
                }
            }
        }
    }
}
