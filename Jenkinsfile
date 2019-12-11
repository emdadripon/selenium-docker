pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //sh
                def mvnHome = tool name: 'Apache Maven 3.6.0', type: 'maven'
                sh "${mvnHome}/bin/mvn -B -DskipTests clean package"
            }
        }
        stage('Build Image') {
            steps {
                //sh
                sh "docker build -t='emdadripon/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    //sh
                    sh "docker login --username=${user} --password=${pass}"
                    sh "docker push emdadripon/selenium-docker:latest"
                }
            }
        }
    }
}