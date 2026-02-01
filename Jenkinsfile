pipeline {
    agent any

    environment {
        IMAGE = "him2100/autoscale-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE% ."
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    bat "echo %PASS% | docker login -u %USER% --password-stdin"
                    bat "docker push %IMAGE%"
                }
            }
        }
    }
}
