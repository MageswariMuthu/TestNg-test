pipeline {
    agent any

    tools {
        maven 'maven3'  // Ensure Maven is configured in Jenkins
        jdk 'java'  // Ensure Java is configured in Jenkins
    }

    environment {
        RECIPIENTS = 'mages.jul6@gmail.com'  // Set email recipients
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MageswariMuthu/TestNg-test.git', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                dir('testng-test-project') {  // Navigate to the correct directory
                    sh 'mvn clean test'
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                dir('testng-test-project') {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            emailext subject: "Jenkins Build Success - ${env.JOB_NAME}",
                     body: "Good news! The build for ${env.JOB_NAME} (#${env.BUILD_NUMBER}) was successful.\nCheck the logs here: ${env.BUILD_URL}",
                     to: "${RECIPIENTS}",
                     attachLog: true
        }
        failure {
            emailext subject: "Jenkins Build Failed - ${env.JOB_NAME}",
                     body: "Oops! The build for ${env.JOB_NAME} (#${env.BUILD_NUMBER}) failed.\nCheck the logs here: ${env.BUILD_URL}",
                     to: "${RECIPIENTS}",
                     attachLog: true
        }
    }
}
