pipeline {
    agent any
    tools {
        maven 'Maven-3.9'
        jdk   'JDK-21'
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build') {
            steps { bat 'mvn clean compile' }
        }
        stage('Package') {
            steps { bat 'mvn package -DskipTests' }
        }
        stage('Run') {
            steps { bat 'java -cp target\\hello-world-1.0-SNAPSHOT.jar hello_world' }
        }
    }
    post
    {
        success
         {
            archiveArtifacts artifacts: 'target/*.jar'
            emailext
            (
                to: 'nikhil.kesarwani.tech@gmail.com',
                subject: "✅ BUILD SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Successful!</h2>
                    <p>Job: ${env.JOB_NAME}</p>
                    <p>Build Number: ${env.BUILD_NUMBER}</p>
                    <p>Status: SUCCESS</p>
                    <p>Check details: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html'
            )
        }
        failure
         {
            emailext
            (
                to: 'nikhil.kesarwani.tech@gmail.com',
                subject: "❌ BUILD FAILED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Failed!</h2>
                    <p>Job: ${env.JOB_NAME}</p>
                    <p>Build Number: ${env.BUILD_NUMBER}</p>
                    <p>Status: FAILURE</p>
                    <p>Check details: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html'
            )
        }
        always 
        {
            echo 'Pipeline finished!'
        }
    }
 }
