pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/sakthipriyan6056/kuber.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t newimage /var/lib/jenkins/workspace/project'
                sh 'sudo docker tag newimage sakthipriyank/newimg:latest'
                sh 'sudo docker tag newimage sakthipriyank/newimg:${BUILD_NUMBER}'
            }
        } 
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push sakthipriyank/newimg:latest'
                sh 'sudo docker image push sakthipriyank/newimg:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/project/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        } 
    }    
}    
