pipeline {
    agent any

    stages {
        stage('VERIFY BRANCH') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

        // stage('DOCKER BUILD') {
        //     steps {
        //         pwsh 'docker images -a'
        //         pwsh '''
        //           cd azure-vote/
        //           docker images -a
        //           docker build -t jenkins-pipeline .
        //           docker images -a
        //           cd ..
        //         '''
        //     }
        // }

        stage('START THE APPLICATION ON 8000') {
            steps {
                pwsh 'docker-compose up'
            }
            post {
                success {
                    echo 'The application started successfully :)'
                }
                failure {
                    echo 'The application failed to start :('
                }
            }
        }

        // stage('RUN TESTS') {
        //     steps {
        //         pwsh 'pytest ./tests/test_sample.py'
        //     }
        // }

        // stage('STOP THE APPLICATION ON 8000') {
        //     steps {
        //         pwsh 'docker-compose down'
        //     }
        // }
    }
}
