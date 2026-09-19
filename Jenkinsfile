pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/muhammedanim-ui/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    bat 'npm test'
                }
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

The Jenkins console log is attached for reference.""",
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - Run Tests FAILURE - Build #${BUILD_NUMBER}",
                        body: """The Run Tests stage has failed.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: FAILURE

Please check the attached Jenkins console log for details.""",
                        attachLog: true
                    )
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
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    bat 'npm audit'
                }
            }

            post {
                success {
                    emailext(
                        to: 'muhammedanim741@gmail.com',
                        subject: "Jenkins - NPM Security Scan SUCCESS - Build #${BUILD_NUMBER}",
                        body: """The NPM Audit security scan completed successfully.

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
                        subject: "Jenkins - NPM Security Scan FAILURE - Build #${BUILD_NUMBER}",
                        body: """The NPM Audit security scan has reported vulnerabilities or failed.

Project: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Status: FAILURE

Please review the attached Jenkins console log for the NPM Audit results.""",
                        attachLog: true
                    )
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
