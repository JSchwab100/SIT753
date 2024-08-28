pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven....'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit Tests using JUnit...'
                echo 'Running Integration Tests using TestNG...'
            }
            post {
                success {
                    emailext(
                        to: "jamesrobschwab@gmail.com",
                        subject: "Unit and Integration Tests Passed",
                        body: "The Unit and Integration Tests stage passed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: "jamesrobschwab@gmail.com",
                        subject: "Unit and Integration Tests Failed",
                        body: "The Unit and Integration Tests stage failed. Please check the logs.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code using SonarQube...'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan using OWASP Dependency-Check...'
            }
            post {
                success {
                    emailext(
                        to: "jamesrobschwab@gmail.com",
                        subject: "Security Scan Passed",
                        body: "The Security Scan stage passed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: "jamesrobschwab@gmail.com",
                        subject: "Security Scan Failed",
                        body: "The Security Scan stage failed. Please check the logs.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to Staging using AWS CLI...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging using Selenium...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to Production using AWS CLI...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
