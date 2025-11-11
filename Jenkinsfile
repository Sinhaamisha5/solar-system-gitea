pipeline {
    agent any
    
    tools   {
        nodejs 'node-js24'
            }       
    stages {
        stage('Installing dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --no-audit'
            }
        }
    }
}

