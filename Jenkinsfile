pipeline {
    agent any
    tools{
        maven 'M3'
    }
    stages {
        stage('Cloing Code') {
            steps {
                git changelog: false, poll: false, url: 'https://github.com/abnavemangesh22/devsecwebapp.git'
            }
        }
        stage('code compile'){
            steps {
                sh 'mvn compile'
            }
        }
        stage('sonar-analysys'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube'){
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Upload'){
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'target/WebApp.war', type: 'jar']], credentialsId: 'nexus', groupId: 'lu.amazon.aws.demo', nexusUrl: '192.168.195.11:49154', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
                }
            }
        }
       
    }
}
