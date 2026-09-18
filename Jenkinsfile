```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out the source code from GitHub.'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies.'
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit and integration tests.'
                bat 'npm test'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating code coverage report.'
                bat 'npm run coverage'
            }
        }

        stage('NPM Audit') {
            steps {
                echo 'Running NPM security audit.'
                bat 'npm audit --audit-level=high'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([
                    string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')
                ]) {
                    bat '''
                        echo Starting SonarCloud Analysis...

                        curl -L -o sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.1.0.6387-windows-x64.zip

                        powershell -Command "Expand-Archive -Path sonar-scanner.zip -DestinationPath . -Force"

                        sonar-scanner-7.1.0.6387-windows-x64\\bin\\sonar-scanner.bat
                    '''
                }
            }
        }
    }
}
```
