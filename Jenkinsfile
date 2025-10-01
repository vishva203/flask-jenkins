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
                withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u vishva203 --password-stdin'
                    sh 'docker tag flask-jenkins-demo vishva203/flask-jenkins-demo:latest'
                    sh 'docker push vishva203/flask-jenkins-demo:latest'
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

