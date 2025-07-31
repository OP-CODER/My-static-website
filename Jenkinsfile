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
                // Assuming you have JMeter .jmx scripts in the repo
                sh '/path/to/jmeter -n -t scripts/perftest.jmx -l results.jtl'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Adjust path as needed for your Tomcat setup
                sh '''
                cp target/my-static-website.war /c/Tomcat/apache-tomcat-9.0.107/webapps/
                '''
            }
        }
    }
}
