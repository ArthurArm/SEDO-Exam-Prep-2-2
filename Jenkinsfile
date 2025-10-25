pipeline {
    agent any

    tools {
        dotnetsdk 'dotnet-6' 
    }

    stages {
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