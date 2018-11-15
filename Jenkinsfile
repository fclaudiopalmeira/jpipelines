//Declarative Pipeline
pipeline {
    agent any
    
    stages {
        stage('Cloning Sources') {
            steps {
                git url: 'https://github.com/fclaudiopalmeira/dotnetcore-helloworld'
            }
        }
        stage('Restoring') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build'
            }
        }
        stage('Test') {
            steps {
                sh """
                cd "$WORKSPACE"/UnitTests
                dotnet test
                """
            }
            post {
                success {
                    emailext(
                subject: "${env.JOB_NAME} on build [${env.BUILD_NUMBER}] has been succesfully deployed.",
                body: "Please check the console output for ${env.JOB_NAME} on [${env.BUILD_URL}] ",
                to: "fclaudiopalmeira@gmail.com"
            )
                }
                failure{
            emailext(
                subject: "${env.JOB_NAME} on build [${env.BUILD_NUMBER}] has failed.",
                body: "Please check the console output for ${env.JOB_NAME} on [${env.BUILD_URL}] ",
                to: "fclaudiopalmeira@gmail.com"
            )
            error('Stopping the JOB!…')
        }

            }
        }
        stage('Build and Publish') {
            steps {
             sh 'dotnet publish'   
            }
        }
        stage('ECHO') {
            steps {
             sh 'echo funciona'   
            }
        }
        stage('ECHO2') {
            steps {
                sh """
                cd /home/ubuntu/target1
                terraform init
                """   
            }
        }

    }
            
}
