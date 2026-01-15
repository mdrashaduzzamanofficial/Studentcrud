pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java21'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mdrashaduzzaman/https://github.com/mdrashaduzzamanofficial/Studentcrud.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t mdrashaduzzaman/java-app:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh '''
                    docker login -u $USER -p $PASS
                    docker push mdrashaduzzaman/java-app:latest
                    '''
                }
            }
        }
    }
}
