pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                sh 'dependency-check.sh --project myapp --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'scp target/myapp.war ec2-user@staging-server:/path/to/deploy/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'curl -s http://staging-server/test'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'scp target/myapp.war ec2-user@production-server:/path/to/deploy/'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'dev-team@example.com',
                subject: "Pipeline Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Build was successful. Check Jenkins for details."
            )
        }
        failure {
            emailext (
                to: 'dev-team@example.com',
                subject: "Pipeline Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Build failed. Check Jenkins for details."
            )
        }
    }
}

