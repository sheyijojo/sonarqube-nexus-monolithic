pipeline {
    agent any

    stages {   
        stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
        
             stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        
            }
        stage('Code Qualty Scan') {

           steps {
                  withSonarQubeEnv('sonar_scanner') {
             sh "mvn -f SampleWebApp/pom.xml sonar:sonar"      
               }
            }
       }
        stage('Quality Gate') {
          steps {
                 waitForQualityGate abortPipeline: true
              }
        }
        stage('push to nexus') {
            steps {
<<<<<<< HEAD
             nexusArtifactUploader artifacts: [[artifactId: 'SampleWebAppArtifact', classifier: '', file: 'SampleWebApp/target/SampleWebApp.war', type: 'war']], credentialsId: 'nexuspassword', groupId: 'SampleWebApp', nexusUrl: 'ec2-54-90-124-33.compute-1.amazonaws.com:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOTS'
=======
            nexusArtifactUploader artifacts: [[artifactId: 'SampleWebAppArtifact', classifier: '', file: 'SampleWebApp/target/SampleWebApp.war', type: 'war']], credentialsId: 'nexuspassword', groupId: 'SampleWebApp', nexusUrl: 'ec2-54-90-124-33.compute-1.amazonaws.com:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '1.0-SNAPSHOTS'
>>>>>>> 5548717cd902c04b6be92005c8ac4aac09eae50e
            }   
            
        }
        
        stage('deploy to tomcat') {
          steps {
             deploy adapters: [tomcat9(credentialsId: 'newtomcatpass', path: '', url: 'http://54.210.46.82:8080')], contextPath: 'myapp', war: '**/*.war'
              
              
          }
            
        }
            
        }
} 
