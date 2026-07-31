pipeline{
    agent any
    stages{
        stage('Stage: Build'){
            agent{
                docker{
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm ci
                    npm run build
                    if test -d "duong/dan/thu/muc"; then
                        echo "Yes"
                    fi
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