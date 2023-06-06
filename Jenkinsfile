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
        always {
            junit 'results/*_result.xml'
            cleanWs()
            emailext subject: 'Resultado de la construcción',
                      body: 'Hola,\n\nLa construcción ha finalizado.',
                      to: 'quesadaao@hotmail.com',
                      from: 'quesadaao@hotmail.com'
        }
    }
}
