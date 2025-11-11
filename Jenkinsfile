pipeline {
    agent any

    tools {
        nodejs 'node-js24'
          }

    stages {
        
        stage('Install Dependencies') {
            steps {
                echo '📦 Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('MongoDB Connectivity Test') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'mongo-db-credentials',
                    usernameVariable: 'MONGO_USERNAME',
                    passwordVariable: 'MONGO_PASSWORD'
                )]) {
                    sh '''
                        echo "🔍 Testing MongoDB connection..."
                        export MONGO_URI="mongodb+srv://${MONGO_USERNAME}:${MONGO_PASSWORD}@supercluster.d83jj.mongodb.net/superData?retryWrites=true&w=majority"
                        node app-test.js
                    '''
                }
            }
        }
    }
}
