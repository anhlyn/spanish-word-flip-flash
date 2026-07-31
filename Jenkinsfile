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
        stage('Start Server'){
            agent{
                docker{
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm run dev &
                    echo "Waiting for server startup..."
                    node -e '
                    const http = require("http");
                    const check = () => {
                        http.get("http://localhost:8080", (res) => {
                        process.exit(0);
                        }).on("error", () => {
                        setTimeout(check, 2000);
                        });
                    };
                    check();
                    '
                    echo "Server is ready!"
                '''
            }
        }
    }
}