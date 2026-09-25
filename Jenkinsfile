pipeline {

    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/saranyaAWS/threetier-project.git'
            }
        }

        stage('Build Frontend') {
            steps {
                sh '''
                cd Frontend
                docker build -t saranya751/threetier-frontend:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Build Backend') {
            steps {
                sh '''
                cd Backend
                docker build -t saranya751/threetier-backend:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                docker push saranya751/threetier-frontend:${BUILD_NUMBER}
                docker push saranya751/threetier-backend:${BUILD_NUMBER}
                '''
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                sh '''
                kubectl apply -f k8s/
                '''
            }
        }
    }
}
