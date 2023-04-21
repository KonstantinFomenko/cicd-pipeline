pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/KonstantinFomenko/cicd-pipeline', branch: 'main')
      }
    }

  }
  environment {
    registry = 'konstantinfomenko/cicd-pipeline-task'
  }
}