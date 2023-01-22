pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('JenkinsToDocker')
    }


    stages {
        stage('Building') {
            steps {
              bat 'pip3 install -r Archive/requirements.txt'
            }
        }
        stage('Testing') {
            steps {
              sh 'python3 Archive/test_main.py '
            }
        }
        stage('Deploying'){
            steps {
              sh 'docker build -t jenkins:latest .'
            }
        }
        stage('Running'){
            steps {
              sh 'docker run -d -p 8003:8080 jenkins:latest'
            }
        }
        stage('Login') {

        steps {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push image to Hub'){
            steps{
            sh 'docker push jenkins:latest'
        }
        }
    }

  post{
      always{
         sh 'docker logout'
      }
  }
}
