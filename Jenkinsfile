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

stage('SonarCloud Analysis') {
    steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
            bat '''
                echo Starting SonarCloud Analysis...

                curl -L -o sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.1.0.6387-windows-x64.zip

                powershell -Command "Expand-Archive -Path sonar-scanner.zip -DestinationPath . -Force"

                sonar-scanner-7.1.0.6387-windows-x64\\bin\\sonar-scanner.bat
            '''
        }
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