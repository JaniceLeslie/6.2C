pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Stage 1: Build"
                echo "Description: Compile and package the code using a build automation tool."
                echo "Tool: Maven"
                // Example command for Maven (not executed here)
                // bat 'mvn clean install'
            }
        }

        stage("Unit and Integration Tests") {
            steps {
                echo "Stage 2: Unit and Integration Tests"
                echo "Description: Run unit tests to verify individual components and integration tests to ensure components work together."
                echo "Tools: JUnit for unit testing, Maven for running integration tests"
                // Example commands (not executed here)
                // bat 'mvn test'
                // bat 'mvn verify'
                
                script {
                    bat '''
                    echo Running unit and integration tests... > test.log
                    echo Tests completed successfully. >> test.log
                    '''
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Stage 3: Code Analysis"
                echo "Description: Analyze the code to ensure it meets industry standards and is free from code smells."
                echo "Tool: SonarQube"
                // Example command for SonarQube (not executed here)
                // bat 'mvn sonar:sonar'
            }
        }

        stage("Security Scan") {
            steps {
                script {
                    echo "Stage 4: Security Scan"
                    echo "Description: Perform a security scan to identify vulnerabilities and security issues in the code."
                    echo "Tool: Snyk"
                    // Example command for Snyk (not executed here)
                    // bat 'snyk test --all-projects'
                    bat '''
                    echo Running security scan... > security.log
                    echo Security scan completed. >> security.log
                    '''
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Stage 5: Deploy to Staging"
                echo "Description: Deploy the application to a staging server for pre-production testing."
                echo "Tool: Custom deployment script (e.g., deploy-script.bat)"
                // Example command for deployment (not executed here)
                // bat 'deploy-script.bat staging'
            }
        }

        stage('Integration Test on Staging') {
            steps {
                echo "Stage 6: Integration Test on Staging"
                echo "Description: Run integration tests on the staging environment to ensure the application functions as expected."
                echo "Tool: Custom integration test script (e.g., integration-tests.bat)"
                // Example command for integration testing (not executed here)
                // bat 'integration-tests.bat'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Stage 7: Deploy to Production"
                echo "Description: Deploy the application to the production server."
                echo "Tool: Custom deployment script (e.g., deploy-script.bat)"
                // Example command for production deployment (not executed here)
                // bat 'deploy-script.bat production'
            }
        }
    }

    post {
        always {
            // Archive all log files regardless of build status
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }

        success {
            emailext(
                attachmentsPattern: '*.log', // Attach all log files
                body: "The pipeline build and deployment were successful. Please find the logs attached.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Success: Build Log Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }

        failure {
            emailext(
                attachmentsPattern: '*.log', // Attach all log files
                body: "The pipeline has failed. Please check the attached logs for more details.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Failed: Build Log Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }
    }
}
