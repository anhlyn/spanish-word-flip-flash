pipeline{
    agent any
    stages{
        stage('Start Server'){
            agent{
                docker{
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm ci
                    npm run dev &
                    echo "Waiting for server startup..."
                    until curl -I http://localhost:8080; do
                    sleep 2
                    done
                '''
            }
        }
        stage('This is stage 02'){
            steps{
                sh 'echo "STAGE 02 HERE"'
            }
        }
    }
}