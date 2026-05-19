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
            sh '''
            curl -H "Content-Type: application/json" -X POST -d '{"text":"Build correcta"}' https://discord.com/api/webhooks/1506417334355624028/taEWZXj0eqP9Bspw5QsfsZmsBG1mxc6-LuJbysl_3bO1CFZa8BGJEFMRs8sArMC4H6Xn'''
        }
        failure {
            mail(
                to: 'rikyfo2005@gmail.com',
                subject: 'Build Failed',
                body: 'The build failed. Please check the Jenkins console for details.'
            )
                        sh '''
            curl -H "Content-Type: application/json" -X POST -d '{"text":"Build incorrecta"}' https://discord.com/api/webhooks/1506417334355624028/taEWZXj0eqP9Bspw5QsfsZmsBG1mxc6-LuJbysl_3bO1CFZa8BGJEFMRs8sArMC4H6Xn'''
        }
        always {
            junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}