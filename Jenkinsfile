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
            curl -H "Content-Type: application/json" \
            -X POST \
            -d '{"content":"Build correcta"}' \
            "https://discord.com/api/webhooks/1506423030618787941/g2UdPaNXIXbJqHwAEDE5opFa1-U21C8A5KO7CevRhqzOSjghfVdRX0IMmpe92Z9c4RbP"
            '''
        }

        failure {

            mail(
                to: 'rikyfo2005@gmail.com',
                subject: 'Build Failed',
                body: 'The build failed. Please check the Jenkins console for details.'
            )

            sh '''
            curl -H "Content-Type: application/json" \
            -X POST \
            -d '{"content":"Build incorrecta"}' \
            "https://discord.com/api/webhooks/1506423030618787941/g2UdPaNXIXbJqHwAEDE5opFa1-U21C8A5KO7CevRhqzOSjghfVdRX0IMmpe92Z9c4RbP"
            '''
        }

        always {
            junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}