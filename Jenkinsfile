pipeline {
    agent any
    environment { 
        imageName = "donchayut/hello-nginx"
    }
    stages {
        stage("Prepare"){
            steps {
                echo "Hello World"
            }
        }
        stage("check version"){
            steps {
                sh "docker --version"
            }
        }
        stage("build image"){
            steps {
                sh "docker build -t ${env.imageName} ."
                sh "docker tag ${env.imageName} ${env.imageName}:1.${env.BUILD_NUMBER}"
            }
        }
        stage("Push image"){
            steps {
                
                sh "docker login -u donchayut -p 45213027"
                sh "docker push ${env.imageName}"
               
            }
        }

    }
}

