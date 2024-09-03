pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Initiating the build process: retrieving source code from the specified directory path."
                echo "Proceeding to compile the code and produce the required build artifacts."
                echo "Tool: Maven"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Executing unit tests to validate individual components."
                echo "Performing integration tests to verify interactions between components."
                echo "Tools: JUnit for unit tests, Selenium for integration tests."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Analyzing the codebase to ensure it meets the quality standards."
                echo "Tool: SonarQube for static code analysis."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Conducting a security scan to detect potential vulnerabilities in the code."
                echo "Tool: OWASP Dependency-Check for vulnerability analysis."
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Task: Deploy the application to the staging server."
                echo "Tool: Jenkins Deploy Plugin or SCP command to deploy to AWS EC2."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Executing integration tests within the staging environment to mimic production conditions."
                echo "Tools: Postman or Newman for API testing on staging."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Commencing deployment of the application to the production environment as defined."
                echo "Tool: Jenkins Deploy Plugin or custom scripts for AWS EC2 deployment."
            }
        }
    }

    post {
        success {
            emailext(
                to: 'pautangpua2020@gmail.com',
                subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <p>Good news!</p>
                <p>The build was successful.</p>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>View details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                attachLog: true
            )
        }
        failure {
            emailext(
                to: 'pautangpua2020@gmail.com',
                subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <p>Unfortunately, the build failed.</p>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>View details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                attachLog: true
            )
        }
    }
}
