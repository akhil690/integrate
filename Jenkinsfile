pipeline {
    agent any
    
    environment {
        
        dotnet='C:\Program Files\dotnet'
        awscli = "C:\Program Files\Amazon\AWSCLIV2"
    }

    stages {
        stage('Checkout') {
            steps {
             git 'https://github.com/dungipravalikareddy/msbuild_project.git'   
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\prav1\ConsoleApp\ConsoleApp\ConsoleApp.csproj'
            }
        stage('Clean') {
            steps {
                bat 'dotnet clean C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\prav1\ConsoleApp\ConsoleApp\ConsoleApp.csproj'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\prav1\ConsoleApp\ConsoleApp\ConsoleApp.csproj --configuration Release'
            }
        }
        stage('Unit Test') {
            steps {
                bat 'dotnet test C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\prav1\ConsoleApp\ConsoleApp\ConsoleApp.csproj'
            }
        }
        stage('Publish') {
            steps {
                bat 'dotnet publish C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\prav1\ConsoleApp\ConsoleApp\ConsoleApp.csproj'
        }
        
       
        stage('Uploading') {
               steps {
      // you need cloudbees aws credentials
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'c7404c17-3b93-4e2d-8b86-4f1a2ce6bdb2', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                    bat 'aws s3 ls'
                    bat 'aws s3 cp C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\bin\\Debug\\netcoreapp3.1\\ConsoleApp.dll  s3://awscli-upload/hi/ConsoleApp.dll'
                }
            }
        }
    }
}
