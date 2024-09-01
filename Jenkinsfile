pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'src'
        TESTING_ENVIRONMENT = 'Staging'
        PRODUCTION_ENVIRONMENT = 'PauProduction'
        EMAIL_RECIPIENT = 'pautangpua2020@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests with JUnit and integration tests"
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Performing code analysis using SonarQube"
                sh 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP ZAP"
                sh 'zap-cli quick-scan http://your-app-url'
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
                sh 'scp target/app.war ec2-user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment"
                sh './run-staging-tests.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment: ${PRODUCTION_ENVIRONMENT}"
                sh 'scp target/app.war ec2-user@prod-server:/path/to/deploy'
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
