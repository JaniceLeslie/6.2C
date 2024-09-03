pipeline {
    agent any
    environment {
        DIRECTORY_PATH = 'C:/ProgramData/Jenkins/.jenkins/workspace/6.2c'
        TESTING_ENVIRONMENT = 'test-env'
        PRODUCTION_ENVIRONMENT = 'Janice'
    }
    stages {
        stage('Build') {
            steps {
                echo "Stage 1: Build"
                echo "Description: Compile and package the code using a build automation tool."
                echo "Tool: Maven"
                // Example command for Maven (not executed here)
                // sh 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Stage 2: Unit and Integration Tests"
                echo "Description: Run unit tests to verify individual components and integration tests to ensure components work together."
                echo "Tools: JUnit for unit testing, Maven for running integration tests"
                // Example commands (not executed here)
                // sh 'mvn test'
                // sh 'mvn verify'
            }
            post {
                success {
                    script {
                        emailext(
                            attachmentsPattern: '*.log',
                            body: "Unit and Integration Tests were successful. Please check the attached log for details.",
                            recipientProviders: [culprits(), developers()],
                            subject: "Pipeline Success - Unit and Integration Tests",
                            to: "30568janiceleslie74@gmail.com"
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            attachmentsPattern: '*.log',
                            body: "Unit and Integration Tests failed. Please check the attached log for details.",
                            recipientProviders: [culprits(), developers()],
                            subject: "Pipeline Failed - Unit and Integration Tests",
                            to: "30568janiceleslie74@gmail.com"
                        )
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Stage 3: Code Analysis"
                echo "Description: Analyze the code to ensure it meets industry standards and is free from code smells."
                echo "Tool: SonarQube"
                // Example command for SonarQube (not executed here)
                // sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Stage 4: Security Scan"
                echo "Description: Perform a security scan to identify vulnerabilities and security issues in the code."
                echo "Tool: Snyk"
                // Example command for Snyk (not executed here)
                // sh 'snyk test --all-projects'
            }
            post {
                success {
                    script {
                        emailext(
                            attachmentsPattern: '*.log',
                            body: "Security Scan was successful. Please check the attached log for details.",
                            recipientProviders: [culprits(), developers()],
                            subject: "Pipeline Success - Security Scan",
                            to: "30568janiceleslie74@gmail.com"
                        )
                    }
                }
                failure {
                    script {
                        emailext(
                            attachmentsPattern: '*.log',
                            body: "Security Scan failed. Please check the attached log for details.",
                            recipientProviders: [culprits(), developers()],
                            subject: "Pipeline Failed - Security Scan",
                            to: "30568janiceleslie74@gmail.com"
                        )
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Stage 5: Deploy to Staging"
                echo "Description: Deploy the application to a staging server for pre-production testing."
                echo "Tool: Custom deployment script (e.g., deploy-script.sh)"
                // Example command for deployment (not executed here)
                // sh 'deploy-script.sh staging'
            }
        }
        
        stage('Integration Test on Staging') {
            steps {
                echo "Stage 6: Integration Test on Staging"
                echo "Description: Run integration tests on the staging environment to ensure the application functions as expected."
                echo "Tool: Custom integration test script (e.g., integration-tests.sh)"
                // Example command for integration testing (not executed here)
                // sh 'integration-tests.sh'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Stage 7: Deploy to Production"
                echo "Description: Deploy the application to the production server."
                echo "Tool: Custom deployment script (e.g., deploy-script.sh)"
                // Example command for production deployment (not executed here)
                // sh 'deploy-script.sh production'
            }
        }
    }
    
    post {
        success {
            script {
                // Send email notification for successful pipeline
                emailext(
                    attachmentsPattern: '*.log',
                    body: "Pipeline completed successfully. Please check the attached log for details.",
                    recipientProviders: [culprits(), developers()],
                    subject: "Pipeline Success",
                    to: "30568janiceleslie74@gmail.com"
                )
            }
        }
        failure {
            script {
                // Send email notification for failed pipeline
                emailext(
                    attachmentsPattern: '*.log',
                    body: "Pipeline failed. Please check the attached log for details.",
                    recipientProviders: [culprits(), developers()],
                    subject: "Pipeline Failed",
                    to: "30568janiceleslie74@gmail.com"
                )
            }
        }
    }
}
