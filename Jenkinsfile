pipeline
{
    agent { label "dev-server" }
    stages
    {
        stage("code")
        {
            steps
            {
                git url:"https://github.com/v-aryan/node-todo-cicd.git",branch: "master"
                echo "Code cloning done"
            }
        }
        
        stage("Build & Test")
        {
            steps
            {
                sh "docker build -t node-todo ."
                echo "code has been build and testing is done"
            }
        }
        
        stage("Push")
        {
            steps
            {
                withCredentials([usernamePassword(credentialsId:"dockerHub",usernameVariable:"dockerHubUser",passwordVariable:"dockerHubPass")])
                {
                    sh "echo ${env.dockerHubPass} | docker login -u ${env.dockerHubUser} --password-stdin"
                }
                echo "code has been pushed"
            }
        }
        
        stage("Deploy")
        {
            steps
            {
                sh "docker-compose down && docker-compose up -d"
                echo "code is deployed."
            }
        }
    }
}
