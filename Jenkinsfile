pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs') {
                sh 'npm install'
                sh 'npm rebuild'
                sh 'npm run build --skip-test --if-present'
                }
            }
        }
        
        stage('uniteTest'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs'){
                    sh 'npm run test:coverage && cp coverage/lcov.info lcov.info || echo "Code coverage failed"'
                    archiveArtifacts(artifacts: 'coverage/**', onlyIfSuccessful: true)
                }
            }
        }

        stage('deploy'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs'){
                    withAWS(credentials: 'aws-credentials', region: 'us-east-1'){
                        sh 'serverless deploy'
                    }
                }
            }
        }
    }
}