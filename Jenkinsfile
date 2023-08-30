pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages{
        
        stage('BUILD'){
            steps{
                sh'mv clean install package'
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
