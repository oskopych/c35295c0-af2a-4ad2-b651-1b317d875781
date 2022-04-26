pipeline {
   agent none
   stages {     
    stage('Running Tests') {
        sh """
            docker build \
                --file ./docker/Dockerfile \
                --tag petclinic:0.0.1 \
                --target test
        """
    }       
   }
 }
