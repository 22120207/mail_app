pipeline {
    agent {
        label '22120207'
    }

    evironment {
        PROJECT_NAME = 'mail_app'
        PROJECT_PATH = "${WORKSPACE}/${PROJECT_NAME}"
        REGISTRY_NAME = "tienminhktvn2"
        IMAGE_VERSION =  "${REGISTRY_NAME}/${PROJECT_NAME}_${JOB_NAME}_${BUILD_ID}_#${BUILD_NUMBER}"
        GIT_URL = 'https://github.com/${JOB_NAME}/${PROJECT_NAME}.git'
    }

    stages {
        stage('checkout') {
            steps {
                sh "git clone ${GIT_URL} ${PROJECT_PATH}"
            }
        }
        
        stage('build image') {
            steps {
                sh 'echo whoami'
                sh "cd ${PROJECT_PATH}"
                sh "docker build -t ${IMAGE_VERSION} ."
            }
        }

        stage('push to registry') {
            steps {
                echo "pushing image ${IMAGE_VERSION} to ${REGISTRY_NAME} registry..."
            }
        }

        stage('deploy') {
            steps {
                sh "docker run --rm -dp 3000:3000 --name ${PROJECT_NAME} ${IMAGE_VERSION}"
            }
        }
    }
}