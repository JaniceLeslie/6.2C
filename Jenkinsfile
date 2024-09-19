pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "mvn clean package"
                // Run the Maven clean and package commands
                // sh 'mvn clean package' (replace with actual command)
            }
        }

        stage("Unit and Integration Tests") {
            steps {
                echo "mvn test" 
                // Run Maven tests (unit and integration)
                // sh 'mvn test' (replace with actual command)
            }
        }

        stage("Code Analysis") {
            steps {
                echo "mvn sonar:sonar" 
                // Run code analysis using SonarQube
                // sh 'mvn sonar:sonar' (replace with actual command)
            }
        }

        stage("Security Scan") {
            steps {
                echo "mvn org.owasp:dependency-check-maven:check" 
                // Run security scan using OWASP Dependency-Check
                // sh 'mvn org.owasp:dependency-check-maven:check' (replace with actual command)
            }
        }

        stage("Deploy to Staging") {
            steps {
                echo "aws deploy-to-staging-script.sh"
                // Deploy to the staging environment (e.g., AWS EC2)
                // sh './deploy-to-staging-script.sh' (replace with actual script)
            }
        }

        stage("Integration Tests on Staging") {
            steps {
                echo "mvn verify -Pintegration-tests" 
                // Run integration tests on the staging environment
                // sh 'mvn verify -Pintegration-tests' (replace with actual command)
            }
        }

        stage("Deploy to Production") {
            steps {
                echo "aws deploy-to-production-script.sh"
                // Deploy to the production environment (e.g., AWS EC2)
                // sh './deploy-to-production-script.sh' (replace with actual script)
            }
        }
    }

    post {
        always {
            // Archive logs for both success and failure
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
        
        success {
            emailext(
                attachmentsPattern: '**/*.log', // Attach log files
                body: "The pipeline build and deployment were successful. Please find the logs attached.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Success: Build Log Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }

        failure {
            emailext(
                attachmentsPattern: '**/*.log', // Attach log files
                body: "The pipeline has failed. Please check the attached log for more details.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Failed: Build Log Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }
    }
}
