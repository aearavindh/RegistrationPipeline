pipeline {
    agent any
    tools {
        maven "Maven"   
    }    
    stages {
        stage('Compile-Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Pushing to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'Registration', classifier: 'Registration and Login', file: 'pom.xml', type: 'war']], credentialsId: 'nexus-credentialss', groupId: 'comrades.registration', nexusUrl: '18.224.155.110:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'devopstraining', version: 'REG-1.0'
            }
        }
        stage('Deployment to AWS'){
            steps{
            deploy adapters: [tomcat8(credentialsId: 'tomcatCredentials', path: '', url: 'http://3.15.0.139:8088/')], contextPath: 'Registration', onFailure: false, war: '**/target/*.war'
            }
        }
      }
}
