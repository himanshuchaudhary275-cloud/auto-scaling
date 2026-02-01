pipeline {
    agent any

    environment {
        IMAGE = "him2100/autoscale-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t %IMAGE% .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh 'echo %PASS% | docker login -u %USER% --password-stdin'
                    sh 'docker push %IMAGE%'
                }
            }
        }
    }
}
