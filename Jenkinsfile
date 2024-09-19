pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "Running Maven Build"
                sh 'mvn clean package > build.log 2>&1'  // Redirect console output to a log file
            }
        }

        stage("Unit and Integration Tests") {
            steps {
                echo "Running Unit and Integration Tests"
                sh 'mvn test > test.log 2>&1'  // Capture test output into a log file
            }
        }

        stage("Code Analysis") {
            steps {
                echo "Running Code Analysis with SonarQube"
                sh 'mvn sonar:sonar > sonar.log 2>&1'  // Capture SonarQube output into a log file
            }
        }

        stage("Security Scan") {
            steps {
                echo "Running Security Scan with OWASP Dependency-Check"
                sh 'mvn org.owasp:dependency-check-maven:check > security.log 2>&1'  // Capture security scan output into a log file
            }
        }

        stage("Deploy to Staging") {
            steps {
                echo "Deploying to Staging"
                sh './deploy-to-staging-script.sh > deploy-staging.log 2>&1'  // Capture deployment output into a log file
            }
        }

        stage("Integration Tests on Staging") {
            steps {
                echo "Running Integration Tests on Staging"
                sh 'mvn verify -Pintegration-tests > staging-tests.log 2>&1'  // Capture staging test output into a log file
            }
        }

        stage("Deploy to Production") {
            steps {
                echo "Deploying to Production"
                sh './deploy-to-production-script.sh > deploy-production.log 2>&1'  // Capture production deployment output into a log file
            }
        }
    }

    post {
        always {
            // Archive all logs for later review
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }
        
        success {
            emailext(
                attachmentsPattern: '*.log', // Attach all log files
                body: "The pipeline build and deployment were successful. Please find the logs attached.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Success: Logs Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }

        failure {
            emailext(
                attachmentsPattern: '*.log', // Attach all log files
                body: "The pipeline has failed. Please check the attached logs for more details.",
                recipientProviders: [culprits(), developers()],
                subject: "Pipeline Failed: Logs Attached",
                to: "30568janiceleslie74@gmail.com"
            )
        }
    }
}
