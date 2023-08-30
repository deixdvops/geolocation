pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {
    registry = '518045124624.dkr.ecr.us-east-1.amazonaws.com/devops-repo'
    registryCredential = 'jenkins-ecr'
    dockerimage = ' '

    }
    stages{
        
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/deixdvops/geolocation.git'
            }
        }
        stage('code build'){
            steps{
                sh'mvn clean install package'
            }
        }
        stage('test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Build image'){
            steps{
                script{
                    dockerImage = docker.buid registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('deploy Image'){
            steps{
                script{
                    docker.withRegistry("https://"+registry,"ecr:us-east-1:"+registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
