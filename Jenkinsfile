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
                def dockerImage = docker.build("${registry}:"Build#":${env.BUILD_ID}")
                docker.withRegistry('', 'dockerhub-id') {
                    dockerImage.push()
                }
            }
        }
        post {
            always {
                echo "Docker push operation completed"
            }
            success {
                echo "Docker image pushed successfully"
            }
        }
    }

    }
    environment {
      registry = 'konstantinfomenko/cicd-pipeline-task'
    }
  }
