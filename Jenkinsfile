pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',url: 'https://github.com/vishva203/flask-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-jenkins-demo .'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'echo "Running tests... (You can add pytest here)"'
            }
        }

        stage('Push to DockerHub') {
			steps {
				// Use username + password credentials in Jenkins
				withCredentials([usernamePassword(credentialsId: 'docker-cred', 
												usernameVariable: 'DOCKER_USER', 
												passwordVariable: 'DOCKER_PASS')]) {
					sh '''
						# Login to DockerHub securely
						echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
						
						# Tag the image
						docker tag flask-jenkins-demo $DOCKER_USER/flask-jenkins-demo:latest
						
						# Push to DockerHub
						docker push $DOCKER_USER/flask-jenkins-demo:latest
					'''
				}
			}
			
		}


        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app flask-jenkins-demo'
            }
        }
    }
}

