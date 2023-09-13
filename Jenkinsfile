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
         stage("Sonarque scan"){
            steps{
                withSonarQubeEnv('SONAR_RUNNER') {
                sh'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=deixdvops_geolocation'                }
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
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
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
                //deploy the image that is in ECR to our EKS cluster
        stage ("Kube Deploy to k8s") {
            steps {
                withKubeConfig([credentialsId: 'k8s', serverUrl: '']) {
                 sh "kubectl apply -f eks_deploy_from_ecr.yaml"
                }
            }
        }
            }
        }
    }
}
