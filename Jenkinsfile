pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Checking out from Github'
                git 'https://github.com/abhinallana/todoList-node-cicd.git'
            }
        }
        stage('Docker Build'){
            steps{
                docker build . -t abhinallana/todo-node-app
                echo "Built Success"
            }
        }
        stage('Docker Push'){
            steps{
                docker push abhinallana/todo-node-app:v1
                echo "pushed Success"
            }
        }
        stage('Completed'){
            steps{
                echo "Completed"
            }
        }
    }
}
