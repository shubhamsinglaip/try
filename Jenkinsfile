pipeline {
    agent any
    environment {
     shubham_docker=credentials('shubham_docker')
}
    stages{
        
        stage('stash code'){
            
            
            steps{
                git branch: 'main', url: 'git url: "https://github.com/shubhamsinglaip/Dockerfile-and-app.py.git"'
                stash 'source'
                
                
                script{
                    sh 'echo "stashed successfully"'
                                      
                }
            }
        }
        
        
        stage('Build Docker Image'){
            agent {
                label 'jennode'
            }
            
            
            steps{
                unstash 'source'
                
                script{
                    sh 'docker build -t shubham030899/docker-jenkins-integration .'                   
                }
            }
        }
        stage('Push Image to Dockerhub'){
            agent {
                label 'jennode'
            }
            
            steps{
                stash 'source'
                script{       
                        sh 'docker login -u ${shubham_docker_USR} -p ${shubham_docker_PSW} '
                        sh 'docker push shubham030899/docker-jenkins-integration'
                }
            }
        }
        stage('Pull Image from Hub'){
            agent {
                label 'jennode'
            }
            
            steps{
                stash 'source'
                script{       
                    sh 'docker pull shubham030899/docker-jenkins-integration'
                }
            }
        }
        stage('Start Container'){
            agent {
                label 'jennode'
            }
            
            steps{
                stash 'source'
                script{
                    sh 'docker rm mycontainer'
                    sh 'docker run --name mycontainer shubham030899/docker-jenkins-integration'
                }
            }
        }
    }
}
