pipeline {
    agent any 
    stages {
        stage('ImageBuild') { 
            steps {
                sh "docker build -t demo ."
            }
        }
        stage('ImagePush') { 
            steps {
                sh "\$(aws ecr get-login --no-include-email --region us-east-1)"
                sh "docker tag demo:latest 723008196684.dkr.ecr.us-east-1.amazonaws.com/dummy-testing:${BUILD_NUMBER}"
                sh "docker push 723008196684.dkr.ecr.us-east-1.amazonaws.com/dummy-testing:${BUILD_NUMBER}"
            }
        }
        stage('Approval') {
           input{
               message "Do you want to proceed for production deployment?"
            }             
        }
        stage('Deploy') { 
            steps {
                sh "echo ${BUILD_NUMBER}"
                sh "sed -i '/723008196684.dkr.ecr.us-east-1.amazonaws.com/s/tag/${BUILD_NUMBER}/' deployments.yml"
                sh "kubectl apply -f deployments.yml --kubeconfig=kube/fourkites-common-eks-dev-cluster" 
            }
        }
    }
}
