pipeline {
    agent any
    tools {
        jdk "java 11"
        maven "maven"
    }
    stages{
        stage('git checkout'){
            steps{
            git branch: 'main', url: 'https://github.com/prajnap46/test-1.git'
            }
        }
        stage('compile the code'){
            steps{
                sh "mvn compile"
            }
        }
        stage('build'){
            steps{ 
                sh "mvn clean install"

            }
        }

    }
}