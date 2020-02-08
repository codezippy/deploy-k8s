pipeline {
    agent any 
    stages {
        stage('ImageBuild') { 
            steps {
                sh "docker build -t demo ."
            }
        }
        stage('Test') { 
            steps {
                sh "echo hello"
            }
        }
        stage('Deploy') { 
            steps {
                sh "echo hello" 
            }
        }
    }
}
