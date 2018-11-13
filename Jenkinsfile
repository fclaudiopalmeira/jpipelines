//Declarative Pipeline
pipeline {
    agent any

    stages {
        stage('restoring') {
            steps {
                dotnet restore
            }
        }
        stage('Build') {
            steps {
                dotnet Build
            }
        }
        stage('Test') {
            steps {
                cd "$WORKSPACE"/UnitTests
                dotnet test
            }
        }
    }
}
