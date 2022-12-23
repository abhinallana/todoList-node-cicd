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
                sh 'docker build . -t abhinallana/todo-node-app:v2'
                echo "Built Success"
            }
        }
        stage('Docker Push'){
            steps{
                withDockerRegistry([ credentialsId: "dockercreds", url: "" ]) {
                    sh 'docker push abhinallana/todo-node-app:v2'
                    echo "pushed Success"
                    } 
            }
        }
        stage('Deploy to Kubernetes(Minikube)'){
            steps{
                dir("${env.WORKSPACE}/k8s"){
                sh "pwd"
                sh "kubectl apply -f deployment.yaml -n devops"
                sh "kubectl apply -f service.yaml -n devops"
                }
            }
        }
        stage('Completed'){
            steps{
                echo "Completed"
            }
        }
    }
}
