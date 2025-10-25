pipeline {
    agent any

    stages {
        stage('Install .NET 6.0 Runtime') {
            steps {
                sh '''
                    wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
                    chmod +x dotnet-install.sh
                    ./dotnet-install.sh --channel 6.0 --runtime dotnet --install-dir /usr/share/dotnet
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