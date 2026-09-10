pipeline {

    agent any

    stages {

        stage('Clone Code') {

            steps {
              git branch : 'main',
              url : 'https://github.com/VishuReddy-dev/jenkins-demo.git'
            }

        }

        stage('Check Files') {

            steps {
                sh 'pwd'
                sh 'ls -la'
            }

        }
        stage('Cleanup'){
            steps{
                sh 'docker rm -f app1 || true'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t myapp:v1 .'
            }
        }
        stage('Run Container'){
            steps{
                sh 'docker run --name app1 myapp:v1'
            }
        }

    }

}
