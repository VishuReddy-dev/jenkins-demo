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
	stage('Tag'){
		steps{
			sh 'docker tag myapp:v1 vishureddy28/myapp:v1'
		}
	}
	stage('Docker Login'){
		steps{
			withCredentials([
				usernamePassword(
					credentialsId: 'dockerhub-creds',
					usernameVariable: 'DOCKER_USER',
					passwordVariable: 'DOCKER_PASS'
				)
			]){
				sh '''
				echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
				'''
			}
		}
	}
	stage('Push'){
		steps{
			sh 'docker push vishureddy28/myapp:v1'
		}
	}
        stage('Run Container'){
            steps{
                sh 'docker run --name app1 myapp:v1'
            }
        }

    }

}
