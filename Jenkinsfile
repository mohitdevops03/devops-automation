pipeline{
    agent any
    tools {
        maven '3.6.3'
    }
    stages{
        stage('Build Maven'){
        steps {
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mohitdevops03/devops-automation']])
            sh 'mvn clean install'
        }
      }
      stage ('Build Docker Image')
      {
        steps{
            script{
                sh 'docker build -t argocdpoc.azurecr.io/app/v1.02 .'
            }
        }
      }
      stage ('Push Image to ACR')
      {
        steps{
            script{
                withCredentials([string(credentialsId: 'acrpwd', variable: 'acrpwd')]) {
                sh 'docker login argocdpoc.azurecr.io/app/v1.02 -u Argocdpoc -p ${acrpwd}' 
}
                sh 'docker push argocdpoc.azurecr.io/app/v1.02'
            }
        }
      }

    }
}
