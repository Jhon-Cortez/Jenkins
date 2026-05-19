pipeline {
    agent any

    stages {

        stage('Permisos') {
            steps {
                sh 'chmod +x mvnw'
            }
        }

        stage('Build and Test') {
            steps {
                sh './mvnw clean verify'
            }
        }
    }

    post {
        always {
            junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}