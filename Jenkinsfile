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
                sh '''
                    ls -la 
                    npm --version
                    node --version
                    npm ci
                    npm run build
                    ls -la            
                '''
            }
        }
        stage('Testing') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "starting tests"
                    ls
                    grep -q 'Learn Jenkins' public/index.html && echo "String found" || echo "String not found"
                    npm test          
                '''
            }
        }
    }
}