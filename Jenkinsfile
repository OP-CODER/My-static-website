pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'No build needed for static site'
            }
        }

        stage('Deploy') {
            steps {
                bat 'mkdir -p /var/www/html/'
                bat 'cp -r * /var/www/html/'
                echo 'Website deployed to local folder'
            }
        }
    }
}
