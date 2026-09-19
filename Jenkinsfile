pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application-updated...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
            }
        }

        stage('Staging') {
            steps {
                echo 'Deploying to staging...'
            }
        }

        stage('Integration Test') {
            steps {
                echo 'Running integration tests...'
            }
        }

        stage('Production') {
            steps {
                echo 'Deploying to production...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
