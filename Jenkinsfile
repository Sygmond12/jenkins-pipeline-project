pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' 
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                bat 'dependency-check.bat --project myapp --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'scp target\\myapp.war ec2-user@staging-server:/path/to/deploy/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'curl -s http://staging-server/test'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'scp target\\myapp.war ec2-user@production-server:/path/to/deploy/'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Pipeline Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Build was successful. Check Jenkins for details."
            )
        }
        failure {
            emailext (
                to: 'sygmonddhital@gmail.com',
                subject: "Pipeline Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Build failed. Check Jenkins for details."
            )
        }
    }
}


