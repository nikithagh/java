pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    environment {
        APP_NAME = "java-project-ci"
        RELEASE = "1.0.0"
        DOCKER_USER = "nikitha1997"
        DOCKER_PASS = 'nikitha1997'
        IMAGE_NAME = "${DOCKER_SUER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                echo "cleaning up the workspace"
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/nikithagh/register-app.git'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
        stage("Build and Push Docker Image")
        {
            steps{
                script{
                    docker.withRegistry('',DOCKER_PASS) {
                      docker_image = docker.build "${IMAGE_NAME}"
                        }
                    docker.withRegistry('',DOCKER_PASS) {
                     docker_image.push("${IMAGE_TAG}")
                     docker_image.push('latest')
                    }
                 }
            }
        }
    }
}
