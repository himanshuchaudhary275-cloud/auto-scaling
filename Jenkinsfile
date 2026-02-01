pipeline {
    agent any

    environment {
        IMAGE = "yourdockerhubusername/autoscale-app"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/yourusername/yourrepo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $IMAGE'
                }
            }
        }
    }
}
