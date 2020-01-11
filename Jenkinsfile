pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //bat - for windows
                //sh - for mac
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                //bat
                sh "docker build -t='vinsdocker/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    //bat
			        sh "docker login --username=${user} --password=${pass}"
			        sh "docker push vinsdocker/selenium-docker:latest"
			    }                           
            }
        }
    }
}