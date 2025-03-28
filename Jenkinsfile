pipeline {
    agent any

    tools {
        maven 'maven3'  // Ensure Maven is configured in Jenkins
        jdk 'java'  // Ensure Java is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MageswariMuthu/TestNg-test.git', branch: 'main'
                sh 'ls -R'  // Debugging step: check file structure
            }
        }

        stage('Build & Test') {
            steps {
                dir('testng-test-project') {  // Change directory to where pom.xml is located
                    sh 'pwd'  // Print working directory
                    sh 'ls -la'  // List files for debugging
                    sh 'mvn -B clean test'  // Run Maven in correct directory
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                dir('testng-test-project') {  // Ensure the correct directory
                    junit 'target/surefire-reports/*.xml'  // Locate test reports correctly
                }
            }
        }
    }
}
