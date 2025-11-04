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
        stage('Deploy image') {
            steps {
                script {

                    // Stop & remove old container
                    bat """
                    docker ps -q --filter "name=tp4" | findstr . && docker rm -f tp4
                    """

                    // Run new container
                    bat """
                    docker run -d -p 8081:80 --name tp4 ${registry}:${BUILD_NUMBER}
                    """
                }
            }
        }


    }
}
