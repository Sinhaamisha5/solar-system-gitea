pipeline {
    agent any

    tools {
        nodejs 'node-js24'   // Make sure this matches the NodeJS tool name configured in Jenkins Global Tools
    }

    environment {
        MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
    }

    stages {

        stage('Installing dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --no-audit'
            }
        }

        stage('NPM Dependency Audit') {
            steps {
                echo 'Running npm audit...'
                // Using "|| true" to prevent the build from failing if audit finds vulnerabilities
                sh '''
                    npm audit fix --force || true
                    echo "npm audit exit code: $?"
                '''
            }
        }

        // Uncomment if you want to run OWASP Dependency Check
        /*
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '''
                    --scan ./ 
                    --out ./ 
                    --format ALL 
                    --prettyPrint
                ''', odcInstallation: 'OWASP-DepCheck-11'
                
                dependencyCheckPublisher(
                    failedTotalCritical: 1, 
                    pattern: 'dependency-check-report.xml', 
                    stopBuild: true
                )

                publishHTML([
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: './',
                    reportFiles: 'dependency-check-jenkins.html',
                    reportName: 'Dep Check HTML Report',
                    useWrapperFileDirectly: true
                ])
            }
        }
        */

        stage('Unit Testing') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'mongo-db-credentials', passwordVariable: 'MONGO_PASSWORD', usernameVariable: 'MONGO_USERNAME')]) {
                sh '''
                    echo "MONGO_URI: $MONGO_URI"
                    echo "MONGO_USERNAME: $MONGO_USERNAME"
                    echo "MONGO_PASSWORD: $MONGO_PASSWORD"
                    npm test
                    '''
                }

                //junit allowEmptyResults: true, stdioRetention: '', testResults: 'dependency-check-junit.xml'
            }
        }
    }
}
