pipeline {
    agent any
    environment {
        IMAGE_NAME = "gs1x2/django_demo_template"

    }
    stages {
        stage("test") {
            steps {
                build job: '/lib/django-test-parametrized',
                    parameters: [
                        string(name: 'GIT_URL', value: "${GIT_URL}"),
                        string(name: 'GIT_BRANCH', value: "${GIT_BRANCH}")
                    ]
            }
        }
        stage("build") {
            steps {
                build job: '/lib/django build parametrized',
                    parameters: [
                        string(name: 'GIT_URL', value: "${GIT_URL}"),
                        string(name: 'GIT_BRANCH', value: "${GIT_BRANCH}"),
                        string(name: 'IMAGE_NAME', value: "${IMAGE_NAME}"),
                        string(name: 'GIT_COMMIT_HASH', value: "${GIT_COMMIT}")
                    ]
            }
        }
        stage("push") {
            steps {
                withCredentials(
                [
                    usernamaPassword(usernameVariable: 'LOGIN', passwordVariable: 'PASSWORD', credentialsId: 'dockerhub')
                    ]
                ) {
                    sh 'docker login -u ${LOGIN} -P ${PASSWORD}'
                    sh 'docker push ${IMAGE_NAME}:latest'
                    sh 'docker push ${IMAGE_NAME}:${GIT_COMMIT}'
                }

            }
        }
    }
}