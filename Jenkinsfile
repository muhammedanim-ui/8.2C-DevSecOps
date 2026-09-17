pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build the code using Maven to compile and package the application.'
                echo 'Tool: Maven'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Run unit tests and integration tests to verify the application functionality.'
                echo 'Tool: JUnit'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyse the source code to ensure code quality and industry coding standards.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Perform a security scan to identify vulnerabilities in the application.'
                echo 'Tool: Snyk'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploy the application to a staging server for production-like testing.'
                echo 'Tool: AWS EC2'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on the staging environment to verify application functionality.'
                echo 'Tool: Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploy the application to the production server.'
                echo 'Tool: AWS EC2'
            }
        }
    }
}
