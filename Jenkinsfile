pipeline {
  environment {
    dockerimagename = "rohir/myapp"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/rohitvyawahare/myapp.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
               registryCredential = 'docker-hub-creds'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying webapp to Kubernetes') {
      steps {
        script {
          sh "ls"
          sh 'kubectl apply -f myapp_deploy.yml'
          sh "pwd"
          sh "ip a"
        }
      }
    }
  }
}

