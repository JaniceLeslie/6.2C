pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Building the project... > build.log
                    echo Build completed. >> build.log
                    '''
                }
            }
        }

        stage("Unit and Integration Tests") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Running unit and integration tests... > test.log
                    echo Tests completed successfully. >> test.log
                    '''
                }
            }
        }

        stage("Code Analysis") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Running code analysis... > analysis.log
                    echo Code analysis completed. >> analysis.log
                    '''
                }
            }
        }

        stage("Security Scan") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Running security scan... > security.log
                    echo Security scan completed. >> security.log
                    '''
                }
            }
        }

        stage("Deploy to Staging") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Deploying to staging... > deploy-staging.log
                    echo Deployment to staging completed. >> deploy-staging.log
                    '''
                }
            }
        }

        stage("Integration Tests on Staging") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Running integration tests on staging... > integration-tests.log
                    echo Integration tests on staging completed. >> integration-tests.log
                    '''
                }
            }
        }

        stage("Deploy to Production") {
            steps {
                script {
                    // For Windows use 'bat', for Linux use 'sh'
                    bat '''
                    echo Deploying to production... > deploy-production.log
                    echo Deployment to production completed. >> deploy-production.log
                    '''
                }
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
