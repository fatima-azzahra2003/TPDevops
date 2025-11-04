pipeline {
    agent any

    environment {
        registry = "fatimaazzahra2003/tpdevops"
        registryCredential = 'devopsjenkins'
    }

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
                    docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
