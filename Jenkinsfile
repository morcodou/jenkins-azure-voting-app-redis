pipeline {
    agent any

    stages {
        stage('VERIFY BRANCH') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

        stage('DOCKER BUILD') {
            steps {
                pwsh 'docker images -a'
                pwsh '''
                  cd azure-vote/
                  docker images -a
                  docker build -t jenkins-pipeline .
                  docker images -a
                  cd ..
                '''
            }
        }

        stage('START THE APPLICATION ON 8000') {
            steps {
                pwsh 'docker-compose up -d'
                pwsh './scripts/test_container.ps1'
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

        stage('RUN TESTS') {
            steps {
                pwsh 'pytest ./tests/test_sample.py'
            }
        }

        stage('STOP THE APPLICATION ON 8000') {
            steps {
                pwsh 'docker-compose down'
            }
        }

        stage('PUSH THE CONTAINER') {
            echo "Workspace is $WORKSPACE"
            dir("$WORKSPACE/azure-vote") {
                steps {
                    docker.withRegistry('https://index.docker.io/v1/', 'DockerHub') {
                        def appImage = docker.build('morcodou/jenkins-course:latest')
                        appImage.push()
                    }
                }
            }
        }
    }
}
