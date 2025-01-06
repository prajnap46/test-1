pipeline {
    agent any

    tools {
        jdk 'java-11'  
        maven 'maven'  
    }

    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/prajnap46/test-1.git'
                }
            }
        }

        stage('Compile') {
            steps {
                script {
                    sh "mvn compile"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh "mvn package"
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
        success {
            echo "Build was successful"
        }
        failure {
            echo "Build failed"
        }
    }
}
