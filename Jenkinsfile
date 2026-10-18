
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-web:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f devops-web || true
                    docker run -d --name devops-web -p 8081:80 devops-web:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps --filter name=devops-web'
            }
        }
    }
}
