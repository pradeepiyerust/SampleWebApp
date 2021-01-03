pipeline {
    agent any
    stages {
        stage ('Checkout') {
 	        checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[credentialsId: 'MyGitHub', url: 'https://github.com/pradeepiyerust/SampleWebApp.git']]]) 
	    }
        stage('Resolve dependencies') {
            steps {
                bat "nuget restore SampleWebApp.sln"
            }
        }
        stage('Build') {
            steps {
                bat "\"${tool 'MSBuild'}\msbuild\" SampleWebApp.sln /p:Configuration=Release /t:Clean;Build /p:OutputPath=publish /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
            }
        }
        #stage('Build') {
        #    steps {
        #        zip zipFile: 'SampleWebApp-1.0.0.${env.BUILD_NUMBER}', dir:'publish\_PublishedWebsites\SampleWebApp' 
        #    }
        #}
    }
}