pipeline {
    agent any

    stages {
        
        stage('Verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }       

        stage('Docker build') {
            steps {
                pwsh 'docker images -a'
                pwsh """
                  cd azure-vote/
                  docker images -a
                  docker build -t jenkins-pipeline .
                  docker images -a
                  cd ..
                """
            }
        } 
    }
}
