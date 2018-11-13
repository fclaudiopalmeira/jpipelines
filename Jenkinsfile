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
    post {
        success {
            emailext(
                subject: "${env.JOB_NAME} on build [${env.BUILD_NUMBER}] has been succesfully deployed.",
                body: "Please check the console output for ${env.JOB_NAME} on [${env.BUILD_URL}] ",
                to: "fclaudiopalmeira@gmail.com"
            )
        }   
    }
