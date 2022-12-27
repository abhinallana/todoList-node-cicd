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
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    //sonar-scanner -> name of global config of Sonar Scanner
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv("sonarqube-container") {  //name of configuration
                    sh "${tool("sonar-scanner")}/bin/sonar-scanner \
                     -Dsonar.projectKey=todo-node-app \
                     -Dsonar.sources=. \
                     -Dsonar.host.url=http://172.17.0.2:9000 \
                     -Dsonar.login=admin \
	             -Dsonar.password=admin@123"

               }
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
