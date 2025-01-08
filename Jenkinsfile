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
        stage('Build and tag docker file') {
            steps {
                script {
                    sh "docker build -t prajnap46/project:1 ."
                }
            }
        }
        stage('Containerisation') {
            steps {
                script {
                    sh '''
                        docker stop c1
                        docker rm c1
                        docker run -it -d --name c1 -p 8081:8080 prajnap46/project:1
                    '''
                }
            }
        }
        stage('login to docker hub'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                    echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                    '''
                    }
                }
                    
                      
            }
        }
        stage('Push Image to Docker Repository') {
            steps {
                script {
                    sh 'docker push prajnap46/project:1'
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
