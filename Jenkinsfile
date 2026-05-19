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
        success {
            mail(
                to: 'rikyfo2005@gmail.com',
                subject: 'Build Successful',
                body: 'The build was successful.'
            )
        }
        failure {
            mail(
                to: 'rikyfo2005@gmail.com',
                subject: 'Build Failed',
                body: 'The build failed. Please check the Jenkins console for details.'
            )
        }
        always {
            junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}