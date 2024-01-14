pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }


        //Stage3 : Publish artifacts to nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '29452d18-dc7f-4646-8573-e0f282e34465', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.153:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'AntoniosDevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }

        }
        
        // Stage3 : Publish the source code to Sonarqube
        // Stage3 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'
          //      withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
            //         sh 'mvn sonar:sonar'
                }

            }
        }

        
        
    }