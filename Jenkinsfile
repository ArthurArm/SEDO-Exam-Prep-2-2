pipeline {
    agent any

    environment {
        DOTNET_ROOT = "${WORKSPACE}/dotnet"
        PATH = "${WORKSPACE}/dotnet:${env.PATH}"
    }

    stages {
        stage('Install .NET 6.0 SDK') {
            steps {
                sh '''
                    wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
                    chmod +x dotnet-install.sh
                    ./dotnet-install.sh --channel 6.0 --runtime dotnet-sdk --install-dir $DOTNET_ROOT
                '''
            }
        }
        stage('Restore .NET Packages') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build .NET Project') {
            steps {
                sh 'dotnet build --no-restore --configuration Release'
            }
        }
        stage('Run Unit and Integration Tests') {
            steps {
                sh 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }
    }
}
