pipeline {
    agent any

    environment {
        SONARQUBE = 'MySonarQube' // Configure in Jenkins > Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR-USERNAME/my-static-site.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Nothing to build for static site'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to /var/www/html...'
                sh '''
                    sudo cp -r src/* /var/www/html/
                '''
            }
        }
    }
}
