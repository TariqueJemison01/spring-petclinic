pipeline {
    agent any
    
    triggers {
        cron('H/10 * * * *')
    }
    
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Generate Code Coverage') {
            steps {
                sh 'mvn jacoco:prepare-agent test jacoco:report'
            }
            post {
                always {
                    jacoco(execPattern: '**/target/jacoco.exec')
                    publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'target/site/jacoco', reportFiles: 'index.html', reportName: 'JaCoCo Code Coverage Report'])
                }
            }
        }
    }
}
