pipeline {
    agent any
    
    tools   {
        nodejs 'node-js24'
            }       
    stages {
        stage('VM Node Version') {
            steps {
                echo 'Checking Node and NPM versions...'
                sh '''
                npm --version
                node --version
                '''
            }
        }
    }
}

