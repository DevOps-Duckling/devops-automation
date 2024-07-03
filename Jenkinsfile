pipeline {
    agent any
    tools{
        maven 'maven_3_9_8'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/DevOps-Duckling/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sulehri173/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub--pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u sulehri173 -p ${dockerhubpwd}'

}
                   sh 'docker push sulehri173/devops-integration'
                }
            }
        }
        
        }
    }
