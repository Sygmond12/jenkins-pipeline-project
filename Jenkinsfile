pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                echo 'mvn clean package' //  Maven build command
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'mvn test' // Simulating Maven test command
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
                echo 'curl -s http://staging-server/test' // this is ti simulate integration test command
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'scp target\\myapp.war ec2-user@production-server:/path/to/deploy/' //deploy command
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


