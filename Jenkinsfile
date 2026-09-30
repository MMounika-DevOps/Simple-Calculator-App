pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out Simple Calculator application'
                checkout scm
            }
        }

        stage('Verify Docker') {
            steps {
                sh 'docker --version'
                sh 'docker compose version'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker compose ps'
            }
        }

        stage('Application Test') {
            steps {
                sh 'sleep 10'
                sh 'curl -f http://localhost/api/health'
            }
        }
    }

    post {
        success {
            echo 'Simple Calculator deployed successfully!'
        }

        failure {
            echo 'Deployment failed.'
        }

        always {
            sh 'docker compose ps || true'
        }
    }
}
