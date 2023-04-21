pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/KonstantinFomenko/cicd-pipeline', branch: 'main')
      }
    }

    stage('App Build') {
      steps {
        script {
          sh './cicd-pipeline/scripts/build.sh'
        }

      }
    }

  }
  environment {
    registry = 'konstantinfomenko/cicd-pipeline-task'
  }
}