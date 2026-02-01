
pipeline {
    agent any
    stages {
        stage('Build Image') {
            steps { sh 'docker build -t devops-app .' }
        }
        stage('Run Container') {
            steps { sh 'docker run -d -p 5000:5000 --name devops-app devops-app || true' }
        }
    }
}
