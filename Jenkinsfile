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
          sh 'chmod +x ./scripts/build.sh'
          sh './scripts/build.sh'
        }

      }
    }

    stage('Tests') {
      steps {
        script {
          sh 'chmod +x ./scripts/test.sh'
          sh './scripts/test.sh'
        }

      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry('', 'dockerhub-id') {
            def image = docker.image("${REGISTRY}:${env.BUILD_NUMBER}")
            image.push("${env.BRANCH_NAME}-commit-${env.GIT_COMMIT_SHORT}-${env.GITHUB_URL.replace('https://github.com/', '').replace('.git', '')}")
          }
        }
      }
    }

    }
    environment {
      registry = 'konstantinfomenko/cicd-pipeline-task'
    }
  }
