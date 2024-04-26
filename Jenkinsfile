pipeline {
    agent any

    tools {
        maven "maven-3"
    }

    stages {
        stage('Clean') {
            steps {
                cleanWs()
            }
        }
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/avajait/szkolenie-ci-jenkins-example/tree/main'
            }
        }
      
        stage('Build') {
            steps {
                sh "mvn clean compile"
            }
        }
    }    
        
    post {
        always {
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/TEST-*.xml'
        }
        success {
            slackSend color: "good", iconEmoji: ":jenkins:", message: "Successful build ${env.BUILD_NUMBER} (<${env.BUILD_URL}"
        }
        failure {
            slackSend color: "danger", iconEmoji: ":jenkins:", message: "Failed build ${env.BUILD_NUMBER} (<${env.BUILD_URL}"
        }
    }

}
