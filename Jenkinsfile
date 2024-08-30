pipeline {
    agent any

    tools {
        // Define the build tools
        maven 'Maven-3.6.3' // Ensure Maven is configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Using Maven to build
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                // Running tests using Maven
                sh 'mvn test'
            }
            post {
                always {
                    // Publishing JUnit test results
                    junit 'target/surefire-reports/*.xml'
                }
                success {
                    emailext (
                        to: 'kaniamudhan27@gmail.com',
                        subject: 'SUCCESS in Unit and Integration Tests',
                        body: "Dear Developer,\\n\\nThe Unit and Integration Tests stage has completed successfully.\\n\\nBuild details: ${BUILD_URL}"
                    )
                }
                failure {
                    emailext (
                        to: 'kaniamudhan27@gmail.com',
                        subject: 'FAILURE in Unit and Integration Tests',
                        body: "Dear Developer,\\n\\nThe Unit and Integration Tests stage has failed. Please check the Jenkins logs for more details.\\n\\nBuild details: ${BUILD_URL}"
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Example with SonarQube
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example with OWASP ZAP or other tools
                sh 'zap-cli quick-scan --self-contained --start-options "-config api.disablekey=true" http://localhost:8080'
            }
            post {
                always {
                    emailext (
                        to: 'kaniamudhan27@gmail.com',
                        subject: 'Security Scan Completed',
                        body: "Dear Developer,\\n\\nThe Security Scan stage has completed. Please check the results.\\n\\nBuild details: ${BUILD_URL}"
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Deploy to a staging environment, adjust commands as needed
                sh 'echo Deploying to AWS EC2 instance or similar'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Additional tests in the staging environment
                sh 'echo Integration tests running...'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Deploy to a production environment
                sh 'echo Deploying to AWS EC2 instance or similar'
            }
        }
    }
}
