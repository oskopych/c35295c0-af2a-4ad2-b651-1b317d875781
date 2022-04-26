pipeline {
    agent any
    stages {     
        stage('Running Tests') {
            steps {
                sh """
                    docker build \
                        --file ./docker/Dockerfile \
                        --tag petclinic:0.0.1 \
                        --target test
                """
            }
        }       
    }
 }
