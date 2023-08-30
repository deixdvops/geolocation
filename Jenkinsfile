pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages{
        
        stage('BUILD'){
            steps{
                sh'mvn clean'
                sh'mvn install'
                sh'mvn package'
            }
        }
        stage('Test'){
            steps{
                sh'mv test'
            }
        }
        stage('deploy'){
            steps{
                echo 'deploy step'
            }
        }
    }
}
