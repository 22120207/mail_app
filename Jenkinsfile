pipeline {
    agent {
        label '22120207'
    }

    environment {
        PROJECT_NAME = 'mail_app'
        PROJECT_PATH = "${WORKSPACE}/${PROJECT_NAME}"
        REGISTRY_NAME = "tienminhktvn2"
        IMAGE_VERSION =  "${REGISTRY_NAME}/${PROJECT_NAME}_${JOB_NAME}_${BUILD_ID}_#${BUILD_NUMBER}"
        GIT_URL = 'https://github.com/22120207/mail_app.git'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Add the workspace to safe directories
                    sh "git config --global --add safe.directory ${WORKSPACE}"
                }
                // Clone the repository
                sh "git clone ${GIT_URL} ${PROJECT_PATH}"
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t ${IMAGE_VERSION} ${PROJECT_PATH}"
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    echo "Pushing image ${IMAGE_VERSION} to ${REGISTRY_NAME} registry..."
                    // Add Docker push command if needed
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the Docker container
                    sh "docker run --rm -dp 3000:3000 --name ${PROJECT_NAME} ${IMAGE_VERSION}"
                }
            }
        }
    }
}