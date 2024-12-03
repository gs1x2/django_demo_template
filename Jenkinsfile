pipeline {
    agent {
        docker {
            image 'python:latest'
            args '-u root'
        }
    }
    stages {
        stage('req2') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }
    }
}
