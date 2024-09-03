pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Initiating the build process: retrieving source code from the specified directory path."
                echo "Proceeding to compile the code and produce the required build artifacts."
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Executing unit tests to validate individual components."
                echo "Performing integration tests to verify interactions between components."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Analyzing the codebase to ensure it meets the quality standards."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Conducting a security scan to detect potential vulnerabilities in the code."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Executing integration tests within the staging environment to mimic production conditions."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Commencing deployment of the application to the production environment as defined."
            }
        }
    }

    post {
        success {
            emailext attachLog: true,
            compressLog: true,
            to: 'pautangpua2020@gmail.com',
            body: "The log file for the successful build is available at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastSuccessfulBuild/log",
            subject: "Jenkins Notification: Successful Production Deployment"
        }
        failure {  
            emailext attachLog: true,
            compressLog: true,
            to: 'pautangpua2020@gmail.com',
            body: "The log file for the failed build can be reviewed at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastFailedBuild/log",
            subject: "Jenkins Alert: Production Deployment Failed"
        }
    }
}
