pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs'){
                sh 'npm install'
                sh 'npm build'
                }
            }
        }

        stage('Deploy'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs'){
                    withAWS(credentials: 'aws-credentials'){
                        sh 'serverless deploy'
                    }
                }
            }
        }
    }
}