pipeline {

  environment {
    dockerimagename = "prajwal1327/nodeapp"
    dockerImage = ""
  }

  agent {label 'Build'}

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/prajwal1327/nodeapp_test.git'
      }
    }

    stage('Build image') {
      steps{
         sh 'echo env='
         sh 'docker build -t app1 .'
      }
    }

    stage('Pushing Image') {
      steps {
                sh "df -h"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUSER} -p ${env.dockerHubPassword}"
                sh 'docker tag tomcat_build:${BUILD_VERSION} prajwal1327/app1'
                sh 'docker push prajwal1327/app1'
                }
            }
        } 
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
