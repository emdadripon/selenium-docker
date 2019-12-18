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
                sh "docker build -t='emdadripon/jenkins_test' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'emdadripon', usernameVariable: '$Ctg1025')]) {
                    //sh
			        sh  "docker login --username=${user} --password=${pass}"
			        sh "docker push emdadripon/jenkins_test:latest"
			    }                           
            }
        }
    }
}