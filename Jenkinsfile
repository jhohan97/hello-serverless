pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh 'npm install'
                sh 'npm build'
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