pipeline{
    agent any
    environment {
        IMAGE_NAME="vite:development"
        CONTAINER_NAME="vite-development"
    }
    stages{
        stage("Clone github repo"){
            steps{
                git branch:"master", url:"https://github.com/kamalbhaiii/devops-kamal.git"
            }
        }
        stage("Install dependencies"){
            steps{
                sh "npm install"
            }
        }
        stage("Build the application"){
            steps{
                sh "npm run build"
            }
        }
        stage("Build docker image"){
            steps{
                sh "docker build -t $IMAGE_NAME ."
            }
        }
        stage("Run docker image in Container"){
            steps{
                sh "docker stop $CONTAINER_NAME || true"
                sh "docker remove $CONTAINER_NAME || true"
                sh "docker run -d -p 5173:80 --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }
}