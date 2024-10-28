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

        stage('Tests') {
            parallel {
                stage('Unit Test') {
                agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
                steps {
                    sh '''
                        #test -f build/index.html
                        npm test
                    '''
                }
                post {
        always {
            junit 'jest-results/junit.xml'
        }
        }
        
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    npm install netlify-cli -g
                    netlify --version
                '''
            }
        }
        }
        
    }

    
}
