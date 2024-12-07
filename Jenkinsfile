pipeline {
    agent {
        label '22120207'
    }

    environment {
        PROJECT_NAME = 'mail_app'
        PROJECT_PATH = "${WORKSPACE}"
        REGISTRY_NAME = "tienminhktvn2"
        IMAGE_VERSION =  "${REGISTRY_NAME}/${PROJECT_NAME}_${JOB_NAME}_${BUILD_ID}"
        GIT_URL = 'https://github.com/22120207/mail_app.git'
    }

    stages {
        stage('Checkout') {
            steps {
                sh "echo ${PROJECT_PATH}"
            }
        }

        stage('Build Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_VERSION} ${PROJECT_PATH}"
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    echo "Pushing image ${IMAGE_VERSION} to ${REGISTRY_NAME} registry..."
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "docker run --rm -dp 3000:3000 --name ${PROJECT_NAME} ${IMAGE_VERSION}"
                }
            }
        }
    }
}