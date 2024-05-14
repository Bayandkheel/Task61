pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package' // Adjust this command based on your build tool
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test' // Adjust this command based on your testing framework
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                sh 'mvn sonar:sonar' // Adjust this command based on your code analysis tool
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'snyk test' // Adjust this command based on your security tool
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy' // Adjust this command based on your deployment setup
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'mvn verify' // Adjust this command based on your testing framework
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy' // Adjust this command based on your deployment setup
            }
        }
    }

    post {
        always {
            emailext(
                to: 'developer@example.com',
                subject: "Build ${currentBuild.fullDisplayName}",
                body: "Build ${currentBuild.fullDisplayName} finished with status: ${currentBuild.result}",
                attachLog: true
            )
        }
    }
}
