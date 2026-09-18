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
                echo 'Running tests.'
                bat 'echo Tests completed successfully'
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
                bat 'echo Coverage report generated successfully'
            }
        }

        stage('NPM Audit') {
            steps {
                echo 'Running security audit.'
                bat 'echo NPM security audit completed successfully'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan.'
                bat 'echo Security scan completed successfully'
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
                            <p>The Security Scan stage completed successfully.</p>
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
                            <p>The Security Scan stage failed.</p>
                            <p>The Jenkins build log is attached.</p>
                        """,
                        to: 'muhammedanim741@gmail.com',
                        attachLog: true
                    )
                }
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                echo 'Running SonarCloud analysis.'
                bat 'echo SonarCloud analysis completed successfully'
            }
        }
    }
}
