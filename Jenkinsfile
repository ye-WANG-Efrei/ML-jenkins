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
              bat 'python Archive/test_main.py '
            }
        }
        stage('Build_docker_image'){
            steps {
              bat 'docker build -t jenkins:latest .'
            }
        }
        stage('Running'){
            steps {
              bat 'docker run -d -p 8003:8080 jenkins:latest'
            }
        }
        stage('Login DockerHub') {

        steps {
            bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push image to Hub'){
            steps{
            bat 'docker push jenkins:latest'
        }
        }
    }

  post{
      always{
         bat 'docker logout'
      }
  }
}
