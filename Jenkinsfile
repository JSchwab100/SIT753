pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                sh 'dependency-check.sh --scan . --format XML'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group Staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'mvn verify -Denv=staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group Production'
            }
        }
    }

    post {
        always {
            emailext subject: "Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "Build URL: ${env.BUILD_URL}",
                     recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                     attachLog: true
        }
    }
}
