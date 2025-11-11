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
        stage('NPM Dependency Scan') {
            parallel {
                stage('NPM Dependency Audit') {
                    steps {
                        sh '''
                            npm audit --audit-level=critical
                            echo $?
                        '''
                    }
                }
                stage('OWASP Dependency Check') {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan './'
                            --out './'
                            --format 'ALL'
                            --prettyPrint
                        ''', odcInstallation: 'OWASP-DepCehck-11'
                    }
                }

            }
 
    }
}

