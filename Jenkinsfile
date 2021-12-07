pipeline {
    agent any
    tools {
        maven 'Maven3.8.4-ARDesigns'
    }
    options {
        //To Dicard old build
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3')
        //To print time in logs
        timestamps()
    }

    stages {
        stage('GitcheckoutDeclarativeway'){
            steps{
                git credentialsId: '81dec520-f691-4a32-9669-c478a842c92f', url: 'https://github.com/MQ-Django-organization/maven-web-application.git'
            }
        }
	
        stage('MavenBuildDeclarativeway'){
            steps{
                sh "mvn clean package"
            }
        }
	// Generate Report in SonarQube
        stage('SonarReportDeclarativeway'){
            steps{
                sh "mvn sonar:sonar"
            }
        }
	//Upload Artifcats in to Nexus
        stage('NexusArtifactcreationDeclarativeway'){
            steps{
                sh "mvn deploy"
            }
        }
        /*
        stage('Deploytotomcat'){
            steps{
                sshagent(['ba578d7d-2bc2-4fb6-89be-a2e9de6296f7']) {
                    sh "scp -o StrictHostKeyChecking=no /tmp/maven-web-application.war MQDjangowebuser@clm-pun-uii681:/opt/Tomcat/apache-tomcat-9.0.54/webapps/"
                }
            }
        }*/
    }// Stages Closing
    post {
        always {
	        emailext body: '''Jenkins notification
	        
        	Regards
	        Arshad''', subject: 'Jenkins', to: 'mohammed_arshad@bmc.com'
        }
    }
}//pipeline closing
