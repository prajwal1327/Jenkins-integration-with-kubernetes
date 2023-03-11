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
  }
}
