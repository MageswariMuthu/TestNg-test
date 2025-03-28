pipeline {
    agent any

    tools {
        maven 'maven3'
        jdk 'java'
    }

    environment {
        RECIPIENTS = 'team@example.com'
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
                junit '**/target/surefire-reports/testng-results.xml'  // Updated to use ** wildcard
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            emailext subject: "✅ SUCCESS: Build #${BUILD_NUMBER}",
                     body: """<h3>Build Successful 🎉</h3>
                              <p>Project: ${JOB_NAME}</p>
                              <p>Build Number: ${BUILD_NUMBER}</p>
                              <p>Check logs: <a href="${BUILD_URL}">${BUILD_URL}</a></p>""",
                     to: "${RECIPIENTS}",
                     mimeType: 'text/html'
        }

        failure {
            emailext subject: "❌ FAILURE: Build #${BUILD_NUMBER}",
                     body: """<h3>Build Failed ❌</h3>
                              <p>Project: ${JOB_NAME}</p>
                              <p>Build Number: ${BUILD_NUMBER}</p>
                              <p>Check logs: <a href="${BUILD_URL}">${BUILD_URL}</a></p>""",
                     to: "${RECIPIENTS}",
                     mimeType: 'text/html'
        }
    }
}
