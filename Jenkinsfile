pipeline {
    agent any

    tools {
        maven "maven-3.9.14"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'uat', url: 'https://github.com/spandana-11/maven-webapplication-project-kkfunda.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh "mvn clean package"
            }
        }

        stage('Sonar Report') {
            steps {
                sh "mvn sonar:sonar"
            }
        }
    }

    post {

        started {
            slackSend(
                channel: '#practice-devops',
                color: '#FFFF00',
                message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
            )
        }

        success {
            slackSend(
                channel: '#practice-devops',
                color: '#00FF00',
                message: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
            )
        }

        failure {
            slackSend(
                channel: '#practice-devops',
                color: '#FF0000',
                message: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
            )
        }
    }
}
