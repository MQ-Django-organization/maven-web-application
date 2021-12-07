node{
    def ArshadMaven = tool name: "Maven3.8.4-ARDesigns"
    stage('GetthecodefromGit'){
        git credentialsId: '81dec520-f691-4a32-9669-c478a842c92f', url: 'https://github.com/MQ-Django-organization/maven-web-application.git'
    }
    stage('BuildinMaven'){
        sh "${ArshadMaven}/bin/mvn clean package"
    }
    stage('SonarReport'){
        sh "${ArshadMaven}/bin/mvn sonar:sonar"
    }
    stage('NexusArtifact'){
        sh "${ArshadMaven}/bin/mvn deploy"
    }
    /*
    stage('Deployintotomcat'){
    sshagent(['05f0bd35-16ad-45a5-bf85-b467b690343c']) {
        sh "scp -o StrictHostKeyChecking=no /tmp/maven-web-application.war sonar@clm-pun-uii681:/opt/Tomcat/apache-tomcat-9.0.54/webapps/"
    }
    }*/
}
