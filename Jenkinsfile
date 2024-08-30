pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                echo 'mvn clean package' // Maven build command
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'mvn test' // Simulating what the Maven test command would be
            }
            post {
                always {
                    emailext (
                        to: 'sygmonddhital@gmail.com',
                        subject: "Unit and Integration Tests: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: "Unit and Integration Tests stage completed.\n\nCheck Jenkins for details.",
                        attachLog: true 
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                echo 'mvn sonar:sonar' // Simulate Maven code analysis 
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                echo 'Checking this application for security issues.' // Simulate security scan command
            }
            post {
                always {
                    emailext (
                        to: 'sygmonddhital@gmail.com',
                        subject: "Security Scan: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: "Security Scan stage completed.\n\nCheck Jenkins for details.",
                         attachLog: true //this will send out the log
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'copying to a staging enviroment, for deployment' // Simulating deploy command
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'Now testing application on a staging server' // Simulating integration test command
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'moving files to ec2-user@production-server:/path/to/deploy/' // Deploy command production server in Amazon
            }
        }
    }

    post {
        success {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Pipeline Was Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline build was successful.\n\nCheck Jenkins for details.",
                attachLog: true 
            )
        }
        failure {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Unfortunately Pipeline Has Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline build failed.\n\nCheck Jenkins for details.",
                attachLog: true 
            )
        }
    }
}



