pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t leesullivan24/duo-jenk:latest -t leesullivan24/duo-jenk:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push leesullivan24/duo-jenk:latest
                docker push leesullivan24/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f ./kubernetes
                kubectl set image deployment/flask-deployment flask-container=leesullivan24/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
    }
}
