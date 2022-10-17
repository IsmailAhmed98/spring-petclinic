pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git url: "https://github.com/jfrog/project-examples.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: JFROG-ID,
                    releaseRepo: prac-libs-release-local,
                    snapshotRepo: prac-libs-snapshot-local
                )

                
            }
        }

        stage ('Exec Maven') {
            steps {
                 
                    rtMavenRun (
                        tool: MVN, // Tool name from Jenkins configuration
                        pom: 'pom.xml',
                        goals: 'clean install ',
                        deployerId: "MAVEN_DEPLOYER"
                        
                    )
                }
            }
        

        

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: JFROG-ID
                )
            }
        }
    }
}