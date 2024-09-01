pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'src'
        TESTING_ENVIRONMENT = 'Staging'
        PRODUCTION_ENVIRONMENT = 'PauProduction'
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                // Add Maven build command, e.g., sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests with JUnit and integration tests"
                // Add test commands, e.g., sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing code analysis using SonarQube"
                // Add code analysis command, e.g., sh 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP ZAP"
                // Add security scan command, e.g., sh 'zap-cli scan http://localhost:8080'
            }
            post {
                always {
                    emailext (
                        to: "${EMAIL_RECIPIENT}",
                        subject: "Security Scan Results",
                        body: "The security scan stage has completed. Check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying to the staging environment on AWS EC2"
                // Add deployment command, e.g., sh 'scp target/app.war ec2-user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment"
                // Add integration test command on staging
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment: ${PRODUCTION_ENVIRONMENT}"
                // Add deployment command for production, e.g., sh 'scp target/app.war ec2-user@prod-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            emailext (
                to: "${EMAIL_RECIPIENT}",
                subject: "Pipeline Completed",
                body: "The pipeline has completed all stages. Check the Jenkins logs for details.",
                attachLog: true
            )
        }
    }
}
