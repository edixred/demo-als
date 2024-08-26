pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        IMAGE_NAME = "docker pull desarrolloclave/ktl_con_gwy:1.33.47"
        DEPLOY_SERVER = "usuario@servidor-web"
    }
    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    sh """
                        echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                        docker pull ${IMAGE_NAME}
                    """
                }
            }
        }
        /*stage('Deploy Docker Image') {
            steps {
                script {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${DEPLOY_SERVER} '
                        docker stop web-app || true
                        docker rm web-app || true
                        docker run -d --name web-app -p 8080:80 ${IMAGE_NAME}
                        '
                    """
                }
            }
        }
        stage('Clean Up') {
            steps {
                sh "docker rmi ${IMAGE_NAME}"
            }
        }*/
    }
    post {
        always {
            sh 'docker logout'
        }
        success {
            echo 'Despliegue de web-app completado con éxito.'
        }
        failure {
            echo 'El despliegue de web-app falló.'
        }
    }
}