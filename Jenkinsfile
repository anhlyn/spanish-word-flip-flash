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
        stage('Run Unit Test'){
            agent{
                docker{
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm run test:unit
                '''
            }
        }
        stage('Run E2E Test'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.54.2-noble'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm run test:e2e
                '''
            }
            post{
                always{
                    junit 'reports-e2e/junit.xml'
                    publishHTML(target:[
                        reportName: 'Report - E2E Testing',
                        reportDir: 'reports-e2e/html',
                        reportFiles: 'index.html',
                        allowMissing: false
                    ])
                }
            }
        }
    }
}