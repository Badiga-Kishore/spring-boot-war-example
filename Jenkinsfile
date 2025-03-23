node{
    def mvnHome = tool name : 'maven-3', type:'maven'
    stage('scmcheckout'){
        git credentialsId: '9e9c77d7-b516-4c81-8906-754d39fb0005', url: 'https://github.com/Badiga-Kishore/spring-boot-war-example.git'
    }
    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
    }
    stage('nexusupload'){
        sh "${mvnHome}/bin/mvn clean deploy"
    }
    stage('sonarreport'){
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
     stage('deploytomcat'){
        sshagent(['tomcatserver']) {
    sh "scp -o StrictHostKeyChecking=no target/hello-world*.war ec2-user@44.211.174.127:/opt/apache-tomcat-9.0.102/webapps/"
}
    }
}
