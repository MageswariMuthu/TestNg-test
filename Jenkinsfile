pipeline {
    agent any

    tools {
        maven 'maven3' // Ensure Maven is configured in Jenkins
        jdk 'java'     // Ensure Java is configured in Jenkins
    }

    environment {
        RECIPIENTS = 'team@example.com' // Change to actual email recipients
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MageswariMuthu/TestNg-test.git', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                dir('testng-test-project') {  // Change to the correct subdirectory
                    sh 'mvn clean test'
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'testng-test-project/target/surefire-reports/*.xml'
                archiveArtifacts artifacts: 'testng-test-project/target/*.jar', fingerprint: true
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
