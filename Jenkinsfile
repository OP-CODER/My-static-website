pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube' // 🔧 Must match the name of your SonarQube server in Jenkins
        SITE_PATH = 'C:\\xampp\\htdocs' // ✅ This is the XAMPP web root
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/OP-CODER/My-static-website.git' // 🔧 Replace with your actual repo
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    bat 'sonar-scanner.bat' // ✅ sonar-scanner must be installed and in PATH
                }
            }
        }

        stage('Deploy Website') {
            steps {
                bat """
                    rmdir /S /Q "%SITE_PATH%"
                    mkdir "%SITE_PATH%"
                    xcopy /E /Y src "%SITE_PATH%"
                """
            }
        }

        stage('Done') {
            steps {
                echo 'Your site is now available at http://localhost/'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Static site deployed successfully!'
        }
    }
}
