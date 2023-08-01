pipeline{

    agent any

    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/inam101001/django-notes-app.git" , branch: "main"
                }
            }
        stage("Build"){
            steps { 
                echo "Building the Image"
                sh "docker build -t notes-app ."
                }  
            }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",usernameVariable:"dHubusername",passwordVariable:"dHubpassword")]){
                sh "docker tag notes-app ${env.dHubusername}/notes-app:latest"
                sh "docker login -u ${env.dHubusername} -p ${env.dHubpassword}"
                sh "docker push ${env.dHubusername}/notes-app:latest"
                }
              }
            }
        stage("Deploy"){
            steps {
                echo "Deploying the Container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
