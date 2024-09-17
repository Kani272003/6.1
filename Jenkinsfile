pipeline {
    agent any

    environment {
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        RECIPIENT_EMAIL = 'kaniamudhan2002@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                script {
                    env.BUILD_STATUS = 'SUCCESSFUL' // Status based on actual results
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                script {
                    env.TEST_STATUS = 'PASSED' // Update this based on actual outcomes
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server: ${env.STAGING_SERVER}"
                script {
                    env.STAGING_DEPLOYMENT_STATUS = 'DEPLOYED'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                script {
                    env.STAGING_TESTS_STATUS = 'PASSED'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server: ${env.PRODUCTION_SERVER}"
                script {
                    env.PRODUCTION_DEPLOYMENT_STATUS = 'DEPLOYED'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    env.CODE_ANALYSIS_STATUS = 'COMPLETED'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                script {
                    env.SECURITY_SCAN_STATUS = 'NO VULNERABILITIES FOUND'
                }
            }
        }
    }

    post {
        always {
            echo 'Sending notification email with logs...'
            // Assuming logs are stored in a known file path, modify as necessary
            def logPath = 'build/logs/buildLog.txt' // Update with actual log file path
            def logContent = readFile logPath
            mail to: "${env.RECIPIENT_EMAIL}",
                 subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                 body: """Pipeline execution details:
                          Build Status: ${env.BUILD_STATUS}
                          Test Status: ${env.TEST_STATUS}
                          Code Analysis Status: ${env.CODE_ANALYSIS_STATUS}
                          Security Scan Status: ${env.SECURITY_SCAN_STATUS}
                          Staging Deployment Status: ${env.STAGING_DEPLOYMENT_STATUS}
                          Staging Tests Status: ${env.STAGING_TESTS_STATUS}
                          Production Deployment Status: ${env.PRODUCTION_DEPLOYMENT_STATUS}
                          Logs:
                          ${logContent}
                          See Jenkins for more details."""
        }
    }
}
