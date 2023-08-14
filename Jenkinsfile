pipeline {

  environment {
    dockerimagename = "vcats/nodeapp"
    dockerImage = ""
  }

  agent any

  stages {
	#withDockerContainer('nginx:stable-alpine3.17-slim') {
    #// some block
#}
    stage('Checkout Source') {
      steps {
        git 'https://github.com/vcatss/nodeapp_test.git'
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
               registryCredential = 'dockerhub'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    // stage('Deploying App to Kubernetes') {
    //   steps {
    //     script {
    //       kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
    //     }
    //   }
    // }

  }

}
