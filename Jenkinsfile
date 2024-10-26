pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
                steps {
                    sh '''
                        echo 'Test stage'
                        if cat build/index.html; then
                             echo "File index.html exists and contents are displayed above."
                        else
                             echo "Error: File index.html does not exist."
                             exit 1
                        fi
                        npm test
                    '''
                }
        }
    }
}
