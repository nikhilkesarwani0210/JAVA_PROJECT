pipeline {
    agent any
    tools {
        maven 'Maven-3.9'
        jdk   'JDK-11'
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
    post {
        success { archiveArtifacts artifacts: 'target/*.jar' }
        always  { echo 'Pipeline finished!' }
    }
}