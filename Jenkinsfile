pipeline {
    agent none

    stages {
        stage('Node') {
            agent {
                docker { image 'node:16.13.1-alpine' }
            }
            steps {
                dir ('DotnetTemplate.Web') {
                    sh 'pwd'
                    sh 'node --version'
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }
        stage('.NET') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:6.0' }
            }
            environment {
                DOTNET_CLI_HOME = '/tmp/dotnet_cli_home'
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
    }
}
