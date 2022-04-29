pipeline {
    agent any
    stages {     
        stage('Running Tests') {
            agent {
                // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
                dockerfile {
                    filename 'docker/Dockerfile'
                    dir '.'
                    additionalBuildArgs  '--target test --tag myapp:0.0.1 --build-arg version=1.0.2'
//                     args '--target test --tag myapp:0.0.1'
                }
            }
            steps {
                //This sh step executes pytest’s py.test command on sources/test_calc.py, which runs a set of
                //unit tests (defined in test_calc.py) on the "calc" library’s add2 function.
                //The --junit-xml test-reports/results.xml option makes py.test generate a JUnit XML report,
                //which is saved to test-reports/results.xml
                // sh 'pytest --verbose --junit-xml test-reports/results.xml'
                sh "echo $PWD"
//                 sh """
//                     docker build \
//                         --file ./docker/Dockerfile \
//                         --tag myapp:0.0.1 \
//                         --target test\
//                         .
//                 """
                // sh "mkdir $PWD/reports"
                sh """
                    docker run \
                        -v $WORKSPACE:/output \
                        --rm myapp:0.0.1 \
                        pytest --verbose --junit-xml \
                        /output/results.xml
                """
                sh "ls -al $WORKSPACE"

            }
            post {
                always {
                    //This junit step archives the JUnit XML report (generated by the py.test command above) and
                    //exposes the results through the Jenkins interface.
                    //The post section’s always condition that contains this junit step ensures that the step is
                    //always executed at the completion of the Test stage, regardless of the stage’s outcome.
                    sh "ls -al $WORKSPACE"
                    sh "cat $WORKSPACE/results.xml"

                    junit 'results.xml'
                }
            }
        }       
    }
 }
