pipeline {
    agent any

    stages {
        stage('VM Node Version') {
            steps {
                echo 'Checking Node and NPM versions...'
                sh '''
                    node -v
                    npm -v
                '''
            }
        }
    }
}

