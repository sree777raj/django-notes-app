pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/sree777raj/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t notesapp ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"pipelinedemo",passwordVariable:"pipelinedemopass",usernameVariable:"pipelinedemoUser")]){
                    sh "docker tag notesapp ${env.pipelinedemoUser}/notesapp:latest"
                    sh "docker login -u ${env.pipelinedemoUser} -p ${env.pipelinedemoPass}"
                    sh "docker push ${env.pipelinedemoUser}/notesapp:latest"
                }
              }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000 sree777raj/notesapp:latest"
            }
        }
    }
}

