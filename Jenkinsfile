pipeline {
    agent any

    stages {
        stage('Building') {
            steps {
              sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Testing') {
            steps {
              sh 'python3 -m unittest'
            }
        }
        stage('Deploying'){
            steps {
              sh 'docker build -t <your_image_name> .'
              sh 'docker run -d -p 5000:5000 <your_image_name>'
            }
        }
    }
  triggers{
       githubPush()
  }
}
