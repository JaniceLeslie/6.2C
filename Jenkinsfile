pipeline {
    agent any
    environment {
        DIRECTORY_PATH = 'C:/ProgramData/Jenkins/.jenkins/workspace/5.1p'
        TESTING_ENVIRONMENT = 'test-env'
        PRODUCTION_ENVIRONMENT = 'Janice'
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Building the code with Maven"
                sh 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                sh 'mvn test'
                echo "Running integration tests"
                sh 'mvn verify'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Performing code analysis"
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing security scan"
                sh 'snyk test --all-projects'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging"
                sh 'deploy-script.sh staging'
            }
        }
        
        stage('Integration Test on Staging') {
            steps {
                echo "Running integration tests on staging"
                sh 'integration-tests.sh'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production"
                sh 'deploy-script.sh production'
            }
        }
    }
    
    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
