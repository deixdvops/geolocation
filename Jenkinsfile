pipeline {
    
    triggers {
       pollSCM ('* * * * *')
}
    agent {
        docker { image 'maven:3.8-openjdk-18-slim' }
    tools {
      maven 'M2_HOME'
}

     

    stages {
        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        

        stage('deploy') {
            steps {
                echo 'deploy'
            }
        }
       
    }
}
