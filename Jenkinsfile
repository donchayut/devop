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
                script{
                    docker.withRegistry('http://registry.hub.docker.com','docker-id'){
                        def image=docker.build("${env.imageName}:1.${env.BUILD_NUMBER}")
                        image.push()
                    }
                }
               
            }
        }

    }
}

