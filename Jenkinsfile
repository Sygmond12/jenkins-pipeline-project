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
                echo 'mvn test' // Simulating Maven test command
            }
            post {
                always {
                    emailext (
                        to: 'sygmonddhital@gmail.com',
                        subject: "Unit and Integration Tests: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: "Unit and Integration Tests stage completed.\n\nCheck Jenkins for details.",
                        attachmentsPattern: '**/test-results.xml'
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
                echo 'dependency-check.bat --project myapp --scan .' // Simulate security scan command
            }
            post {
                always {
                    emailext (
                        to: 'sygmonddhital@gmail.com',
                        subject: "Security Scan: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: "Security Scan stage completed.\n\nCheck Jenkins for details.",
                        attachmentsPattern: '**/dependency-check-report.xml'
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'scp target\\myapp.war ec2-user@staging-server:/path/to/deploy/' // Simulating deploy command
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'curl -s http://staging-server/test' // Simulating integration test command
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'scp target\\myapp.war ec2-user@production-server:/path/to/deploy/' // Deploy command
            }
        }
    }

    post {
        success {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Pipeline Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline build was successful.\n\nCheck Jenkins for details."
            )
        }
        failure {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Pipeline Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline build failed.\n\nCheck Jenkins for details."
            )
        }
    }
}



