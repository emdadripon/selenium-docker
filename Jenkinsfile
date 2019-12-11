pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //sh
                sh "mvn clean package -DskipTests"
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
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: '$Ctg1025', usernameVariable: 'emdadripon')]) {
                    //sh
                    sh "docker login --username=${user} --password=${pass}"
                    sh "docker push emdadripon/selenium-docker:latest"
                }
            }
        }
    }
}