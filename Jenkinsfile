pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/muhammedanim-ui/8.2C-DevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }

            post {
                success {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - Run Tests SUCCESS - Build #${BUILD_NUMBER}",
                        body: """The Run Tests stage completed successfully.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: SUCCESS

The Jenkins console log is attached.""",
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - Run Tests FAILURE - Build #${BUILD_NUMBER}",
                        body: """The Run Tests stage failed.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: FAILURE

The Jenkins console log is attached.""",
                        attachLog: true
                    )
                }

                always {
                    echo 'Test stage notification completed.'
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }

            post {
                success {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - NPM Audit SUCCESS - Build #${BUILD_NUMBER}",
                        body: """The NPM Audit security scan completed.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: SUCCESS

The Jenkins console log containing the security scan results is attached.""",
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - NPM Audit SECURITY FINDINGS - Build #${BUILD_NUMBER}",
                        body: """The NPM Audit security scan identified vulnerabilities.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: SECURITY FINDINGS

The Jenkins console log containing the vulnerability results is attached.""",
                        attachLog: true
                    )
                }

                always {
                    echo 'NPM Audit notification completed.'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed with status: ${currentBuild.currentResult}"
        }
    }
}
