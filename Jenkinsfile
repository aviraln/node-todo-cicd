pipeline {
    agent { label "dev agent"}
    stages{
        stage("Code Cloned"){
            steps{
                git url: 'https://github.com/aviraln/node-todo-cicd.git', branch: 'master'
                echo "code cloned"
            }
        }
        stage("Code Build"){
            steps{
                sh 'docker build . -t aviraln/node-todo_cicd:latest'
                echo "code build"
            }
        }
        stage("Docker Login and Push Image"){
            steps{
                echo "login to docker hub and pushing image to it"
                withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh 'docker push aviraln/node-todo_cicd:latest'
                }
            }
        }
        stage("Code Tested"){
            steps{
                echo "code tested"
            }
        }
        stage("Code Deployed"){
            steps{
                echo "code deploying started"
                sh 'docker-compose up -d --no-deps --build web'
                echo "code deployed"
            }
        }
    }
}
