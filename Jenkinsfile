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
                bat 'npm test', returnStatus: true
            }

            post {
                success {
                    emailext(
                        subject: "Jenkins Test Stage - SUCCESS - Build #${env.BUILD_NUMBER}",
                        body: """
                            <h2>Test Stage Successful</h2>
                            <p><b>Project:</b> ${env.JOB_NAME}</p>
                            <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                            <p><b>Status:</b> SUCCESS</p>
                            <p>The Test stage completed successfully.</p>
                            <p>The Jenkins build log is attached.</p>
                        """,
                        to: 'muhammedanim741@gmail.com',
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        subject: "Jenkins Test Stage - FAILURE - Build #${env.BUILD_NUMBER}",
                        body: """
                            <h2>Test Stage Failed</h2>
                            <p><b>Project:</b> ${env.JOB_NAME}</p>
                            <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                            <p><b>Status:</b> FAILURE</p>
                            <p>The Test stage failed.</p>
                            <p>The Jenkins build log is attached.</p>
                        """,
                        to: 'muhammedanim741@gmail.com',
                        attachLog: true
                    )
                }
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

            post {
                success {
                    emailext(
                        subject: "Jenkins Security Scan - SUCCESS - Build #${env.BUILD_NUMBER}",
                        body: """
                            <h2>Security Scan Successful</h2>
                            <p><b>Project:</b> ${env.JOB_NAME}</p>
                            <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                            <p><b>Status:</b> SUCCESS</p>
                            <p>The SonarCloud security analysis completed successfully.</p>
                            <p>The Jenkins build log is attached.</p>
                        """,
                        to: 'muhammedanim741@gmail.com',
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        subject: "Jenkins Security Scan - FAILURE - Build #${env.BUILD_NUMBER}",
                        body: """
                            <h2>Security Scan Failed</h2>
                            <p><b>Project:</b> ${env.JOB_NAME}</p>
                            <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                            <p><b>Status:</b> FAILURE</p>
                            <p>The SonarCloud security analysis failed.</p>
                            <p>The Jenkins build log is attached.</p>
                        """,
                        to: 'muhammedanim741@gmail.com',
                        attachLog: true
                    )
                }
            }
        }
    }
}
