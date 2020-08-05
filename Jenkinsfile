pipeline {
    agent any
    environment {
        registry = 'mhealthvn/test-runner'
        registryCredential = 'mhealthvn'
        dockerImage = ""
    }
    stages{
        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }        
        stage('Deploy Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                       dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:latest"
            }
        }        
    }
}