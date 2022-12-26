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
        stage('Scan with Sonarqube'){
            steps{
                echo 'Scanning with Sonarqube ! Please wait until it completes.'
                sonar-scanner \
                   -Dsonar.projectKey=todo-node-app \
                   -Dsonar.sources=. \
                   -Dsonar.host.url=http://172.17.0.2:9000 \
                   -Dsonar.login=sqp_e6bb5e3d94d0eed49b341abd050ca758759f3f57
            }
        }
        stage('Completed'){
            steps{
                echo "Completed"
            }
        }
    }
}
