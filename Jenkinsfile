pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build commands here
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Testing...'
                // Add your testing commands here
            }
            post {
                success {
                    script {
                        def logFile = archiveArtifacts artifacts: 'tests.log', fingerprint: true
                        emailext (
                            to: 'shrivastavaditi14@gmail.com',
                            subject: 'Success: Unit and Integration Tests',
                            body: """<p>The Unit and Integration Tests stage completed successfully.</p>
                                     <p>See attached log for more details.</p>""",
                            attachmentsPattern: "${logFile}",
                            mimeType: 'text/html'
                        )
                    }
                }
                failure {
                    script {
                        def logFile = archiveArtifacts artifacts: 'tests.log', fingerprint: true
                        emailext (
                            to: 'shrivastavaditi14@gmail.com',
                            subject: 'Failure: Unit and Integration Tests',
                            body: """<p>The Unit and Integration Tests stage failed.</p>
                                     <p>See attached log for more details.</p>""",
                            attachmentsPattern: "${logFile}",
                            mimeType: 'text/html'
                        )
                    }
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities...'
                // Add your security scan commands here
            }
            post {
                success {
                    script {
                        def logFile = archiveArtifacts artifacts: 'securityScan.log', fingerprint: true
                        emailext (
                            to: 'shrivastavaditi14@gmail.com',
                            subject: 'Success: Security Scan',
                            body: """<p>The Security Scan stage completed successfully.</p>
                                     <p>See attached log for more details.</p>""",
                            attachmentsPattern: "${logFile}",
                            mimeType: 'text/html'
                        )
                    }
                }
                failure {
                    script {
                        def logFile = archiveArtifacts artifacts: 'securityScan.log', fingerprint: true
                        emailext (
                            to: 'shrivastavaditi14@gmail.com',
                            subject: 'Failure: Security Scan',
                            body: """<p>The Security Scan stage failed.</p>
                                     <p>See attached log for more details.</p>""",
                            attachmentsPattern: "${logFile}",
                            mimeType: 'text/html'
                        )
                    }
                }
            }
        }
        // Define other stages as needed...
    }
}
