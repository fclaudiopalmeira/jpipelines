//Declarative Pipeline
pipeline {
    agent any
    
    stages {
        stage('Cloning Sources') {
            steps {
                git url: 'https://github.com/fclaudiopalmeira/jpipelines'
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
                to: "email@email.com"
            )
                }
                failure{
            emailext(
                subject: "${env.JOB_NAME} on build [${env.BUILD_NUMBER}] has failed.",
                body: "Please check the console output for ${env.JOB_NAME} on [${env.BUILD_URL}] ",
                to: "email@email.com"
            )
            error('Stopping the JOB!…')
        }

            }
        }
        stage('Build and Publish') {
            steps {
             sh 'dotnet publish --configuration=Release --output "$WORKSPACE"/company/drop/ansible/roles/applic/files'   
            }
        }
        stage('Packer') {
            steps {
                sh """
                cd "$WORKSPACE"/company
                chmod +x ./buildvm.sh
                ./buildvm.sh
                cd "$WORKSPACE"/company/terraform
                chmod +x ./init.sh
                chmod +x ./apply.sh
                ./init.sh
                ./apply.sh
                """   
            }
        }
        
    }
            
}
