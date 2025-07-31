pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Code Quality Check (SonarQube)') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn sonar:sonar \
                      -Dsonar.projectKey=my-static-website \
                      -Dsonar.host.url=http://localhost:9000 \
                      -Dsonar.login=sqa_6a65a46331454db13916b0fbb0c5bd16845c1884
                    '''
                }
            }
        }

        stage('Performance Test (JMeter)') {
            steps {
                sh '''
                /c/apache-jmeter-5.5/bin/jmeter -n -t "/c/Users/mohda/Desktop/Thread Group.jmx" -l "/c/Users/mohda/Desktop/results.jtl"
                '''
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp target/my-static-website.war /c/Tomcat/apache-tomcat-9.0.107/webapps/
                '''
            }
        }
    }
}

