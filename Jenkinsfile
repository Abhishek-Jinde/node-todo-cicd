pipeline {
    agent { label 'Jenkins-agent' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/Abhishek-Jinde/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build'){
            steps {
                sh 'docker build -t abhishekjinde/node-to-do-app-cicd:latest .'
            }
        }
        stage('Docker Login and Push'){
            steps {
                withCredentials([usernamePassword(credentialsId:'Docker-Hub', passwordVariable:'dockerhubPassword', usernameVariable:'dockerhubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push abhishekjinde/node-to-do-app-cicd:latest"
                }
            }
        }
        stage('Deploying'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
