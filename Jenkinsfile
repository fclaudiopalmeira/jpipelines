//Declarative Pipeline
pipeline {
    agent any
    
    stages {
        stage('Cloning Sources') {
            steps {
                git url: 'https://github.com/fclaudiopalmeira/dotnetcore-helloworld'
            }
        }
        stage('restoring') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet Build'
            }
        }
        stage('Test') {
            steps {
                sh """
                cd "$WORKSPACE"/UnitTests
                dotnet test
                """
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
