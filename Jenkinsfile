pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('Local SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=YourProjectKey -Dsonar.login=YourToken'
                }
            }
        }
    }
}
