pipeline {
    agent { label 'slave-1' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/BalajiPyna/node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t balajipyna/sample-docker:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'dockerpassword', usernameVariable: 'dockerusername')]) {
        	     sh "docker login -u ${env.dockerusername} -p ${env.dockerpassword}"
                 sh 'docker push balajipyna/sample-docker:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
