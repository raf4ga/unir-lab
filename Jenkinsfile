pipeline {
    agent any
    stages {
        stage('Check Requirements') {
            steps {
                echo 'Checking requirements...'
            }
        }
        stage('Unit tests') {
            steps {
                echo 'Running unit tests...'
                sh 'make build test-unit'
                archiveArtifacts artifacts: 'results/*.xml'
                archiveArtifacts artifacts: 'results/*.html'
            }
        }
        stage('Api tests') {
            steps {
                echo 'Running API tests...'
                sh 'make build test-api'
                archiveArtifacts artifacts: 'results/*.xml'
                archiveArtifacts artifacts: 'results/*.html'
            }
        }
        stage('E2e tests') {
            steps {
                echo 'Running E2E tests...'
                sh 'make build test-e2e'
                archiveArtifacts artifacts: 'results/*.xml'
                archiveArtifacts artifacts: 'results/*.html'
            }
        }
    }
    post {
        always{
            junit 'results/*_result.xml'
            
            emailext body: 'Test Message',
                    subject: 'Test Subject',
                    to: 'raf4ga@gmail.com'
            echo "Email Notification!"
            echo "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nMore Info can be found here: ${env.BUILD_URL}"
            
            cleanWs()
        }
        failure {
            emailext body: 'Test Message',
                    subject: 'Test Subject',
                    to: 'raf4ga@gmail.com'
            echo "Email Notification!"
            echo "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nMore Info can be found here: ${env.BUILD_URL}"
        }
    }
}
