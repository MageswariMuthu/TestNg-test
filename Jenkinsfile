pipeline {
    agent any

    tools {
        maven 'maven3' // Ensure Maven is configured in Jenkins
        jdk 'java'   // Ensure Java is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MageswariMuthu/TestNg-test.git', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Publish Test Results') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}
