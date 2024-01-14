pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
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
                script {
                
                def NexusRepo = Version.endsWith("SNAPSHOT") ? "AntoniosDevOpsLab-SNAPSHOT" : "AntoniosDevOpsLab-RELEASE"
                nexusArtifactUploader artifacts:
                [[artifactId: "${ArtifactId}",
                classifier: '',
                file: "target/${ArtifactId}-${Version}.war",
                type: 'war']],
                credentialsId: '29452d18-dc7f-4646-8573-e0f282e34465',
                groupId: "${GroupId}",
                nexusUrl: '172.20.10.153:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: "${NexusRepo}",
                version: "${Version}"
                }
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

        // Stage 4 : Print some information
        stage ('print environment variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }
    }

        
        
    }