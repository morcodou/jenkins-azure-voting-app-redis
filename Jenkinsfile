pipeline {
    agent any

    stages {
        stage('VERIFY BRANCH') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

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
    }
}
