pipeline {
    agent {
        docker {
            image 'python:latest'
            args '-u root'
        }
    }
    stages {
        stage("checkout") {
            steps {
                git branch: "${GIT_BRANCH}",
                    credentialsId: "${GIT_CREDENTIAL}",
                    url: "${GIT_URL}"
            }
        }
        stage("deps") {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage("test") {
            steps {
                sh 'coverage run manage.py test'
            }
        }
        stage("reports") {
            steps {
                sh 'coverage report'
                sh 'coverage xml'
                sh 'coverage html'
            }
        }
    }
}

