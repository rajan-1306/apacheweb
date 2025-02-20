pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rajan-1306/apacheweb'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the website..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests (if any)..."'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['apache-server-credentials']) {
                    sh '''
                        ssh user@server-ip "sudo systemctl restart apache2"
                        rsync -avz --delete ./ user@server-ip:/var/www/html/
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
