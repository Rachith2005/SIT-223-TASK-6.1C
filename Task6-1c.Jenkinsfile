pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven.'
                echo 'Tool: Maven'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit.'
                echo 'Tool: JUnit'
                script {
                    def logFile = "unit-test-log.txt"
                    try {
                        echo 'Running unit tests...' > ${logFile}
                        echo 'Simulated log content for Unit and Integration Tests' >> ${logFile}
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Unit and Integration Tests failed. See ${logFile} for details.")
                    }
                }
            }
            post {
                always {
                    script {
                        emailext(
                            to: 'rachithmicrosoft@gmail.com',
                            subject: "Unit and Integration Tests: ${currentBuild.result}",
                            body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.result}. Please find the attached log file for details.",
                            attachmentsPattern: "unit-test-log.txt"
                        )
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code for quality using SonarQube.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities using OWASP Dependency-Check.'
                echo 'Tool: OWASP Dependency-Check'
                script {
                    def logFile = "security-scan-log.txt"
                    try {
                        echo 'Performing security scan...' > ${logFile}
                        echo 'Simulated log content for Security Scan' >> ${logFile}
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Security Scan failed. See ${logFile} for details.")
                    }
                }
            }
            post {
                always {
                    script {
                        emailext(
                            to: 'rachithmicrosoft@gmail.com',
                            subject: "Security Scan: ${currentBuild.result}",
                            body: "The Security Scan stage has completed with status: ${currentBuild.result}. Please find the attached log file for details.",
                            attachmentsPattern: "security-scan-log.txt"
                        )
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to a staging environment using AWS CLI.'
                echo 'Tool: AWS CLI'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment using Selenium.'
                echo 'Tool: Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production using AWS CLI.'
                echo 'Tool: AWS CLI'
            }
        }
    }

    post {
        always {
            echo 'Sending notification after the pipeline is completed.'
            mail(
                to: 'rachithmicrosoft@gmail.com',
                subject: "Build Status: ${currentBuild.result}",
                body: "The pipeline has completed with the status: ${currentBuild.result}"
            )

            emailext(
                to: 'rachithmicrosoft@gmail.com',
                subject: "Pipeline Completed: ${currentBuild.result}",
                body: "The entire pipeline has completed with the status: ${currentBuild.result}. Please find the attached log files for details.",
                attachmentsPattern: "unit-test-log.txt, security-scan-log.txt"
            )
        }
    }
}
