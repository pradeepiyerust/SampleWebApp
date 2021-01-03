pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
 	            checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[credentialsId: 'MyGitHub', url: 'https://github.com/pradeepiyerust/SampleWebApp.git']]]) 
            }
	    }
        stage ('Resolve') {
            steps {
                bat "nuget restore SampleWebApp.sln"
            }
        }
        stage ('Build') {
            steps {
                bat "\"${tool 'MSBuild'}\\msbuild\" SampleWebApp.sln /p:Configuration=Release /t:Clean;Build /p:OutputPath=publish"
            }
        }
        stage('Package') {
            steps {
                bat "del *.zip"
                zip zipFile: "SampleWebApp-1.0.0.${env.BUILD_NUMBER}.zip", dir:"SampleWebApp\\publish\\_PublishedWebsites\\SampleWebApp"
            }
        }
        stage('Deploy') {
            steps {
                unzip zipFile: "SampleWebApp-1.0.0.${env.BUILD_NUMBER}.zip", dir:"D:\\SampleWebApp"
            }
        }
    }
}