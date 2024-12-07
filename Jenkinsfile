pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                sh "git clone ${GIT_URL} ${PROJECT_PATH}"
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
