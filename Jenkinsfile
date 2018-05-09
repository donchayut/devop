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
                    docker.withRegistry('http://docker.io','docker-id'){
                        def image=docker.build("${env.imageName}:1.${env.BUILD_NUMBER}")
                        image.push()
                    }
                }
               
            }
        }
        stage("deploy"){
            steps{
                sshagent(['4890593f-9bf2-41d1-b2eb-f72df8e9f0d3']){
                    echo "ec deploy step"
                    sh "ssh core@167.99.237.229 docker pull doncahyut/hello-nginx"
                }
            }
        }

    }
}

