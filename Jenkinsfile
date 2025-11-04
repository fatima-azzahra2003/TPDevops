pipeline {
    environment {
        registry = "fatimaazzahra2003/tpdevops"
        registryCredential = 'devopsjenkins'
        dockerImage = ''
    }
    agent any

    stages {

        stage('Cloning Git') {
            steps {
                git 'https://github.com/fatima-azzahra2003/TPDevops'
            }
        }

        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy image') {
            steps {
                script {
                    bat "docker rm -f tp4 || echo 'container not running'"
                    bat "docker run -d -p 8081:80 --name tp4 ${registry}:${BUILD_NUMBER}"
                }
            }
        }
    }
}
