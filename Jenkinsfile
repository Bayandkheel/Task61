pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                bat 'snyk test'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                bat 'pscp -i C:\Users\bayan\OneDrive\Desktop\azurs.ppk azureuser@52.170.123.45:/home/azureuser/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                bat 'mvn verify'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                bat 'pscp -i C:\Users\bayan\OneDrive\Desktop\azurs.ppk azureuser@52.170.123.45:/home/azureuser/deploy'
            }
        }
    }

    post {
        always {
            emailext(
                to: 'bayandkheel12@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName}",
                body: "Build ${currentBuild.fullDisplayName} finished with status: ${currentBuild.result}",
                attachLog: true
            )
        }
    }
}
