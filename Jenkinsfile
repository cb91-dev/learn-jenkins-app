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
        stage('Unit Testing') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "starting tests"
                    grep -q 'Learn Jenkins' public/index.html && echo "String found" || echo "String not found"
                    npm test          
                '''
            }
        }
        stage('E2E Testing') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
        }
    }
}