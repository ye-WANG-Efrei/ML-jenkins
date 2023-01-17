pipeline {
    agent any
 
    options {
        skipDefaultCheckout(true)
    }
 
    stages {
        stage('Checkout SCM') {
            steps {
                echo '> Checking out the source control ...'
                checkout scm
            }
        }
        stage('Git Pull') {
            steps {
                echo '> Pulling the code from GitHub repository ...'
                sh 'git remote update && git checkout develop && git pull origin develop'
            }
        }
        stage('Docker Up') {
            steps {
                echo '> Building the docker containers ...'
                sh 'cd docker && cd ci && make build'
            }
        }
        stage('Composer Install') {
            steps {
                echo '> Building the application within the container ...'
                sh 'cd docker && cd ci && make composer'
            }
        }
        stage('Test') {
            steps {
                echo '> Running the application tests ...'
                sh 'cd docker && cd ci && make test'
            }
        }
    }
}
