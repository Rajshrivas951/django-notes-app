pipeline{
    agent any
    stages{
        stage("clone code"){
            steps{
                echo "Clonig code"
                git url:"https://github.com/Rajshrivas951/django-notes-app.git", branch: "main"
                
            }
            
        }
        stage("Build"){
            steps{
                echo "Build the image"
                sh "docker build -t notess-app . "
            }
            
        }
        stage("Push to DockerHub"){
            steps{
                echo "pushing to DockerHUb"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notess-app ${env.dockerHubUser}/notess-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notess-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "deploying"
                sh"docker-compose down && docker-compose up -d"
                
            }
            
        }
    }
}
