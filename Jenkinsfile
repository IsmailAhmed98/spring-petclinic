pipeline{
    agent any
    tools {maven 'MVN'}
    triggers{
        pollSCM('* * * * *') 
    }
    stages{
        stage('clone'){
            steps{
                git branch:'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('Artifactory'){
            steps{
                rtMavenDeployer(
                    id: 'MVN_DEPLOYER',
                    serverId: "JFROG_INSTANCE",
                    releaseRepo: "isma-libs-release-local",
                    snapshotRepo: "isma-libs-snapshot-local" 
                    )
            }
        }
        stage('SONARQUBE'){
            steps{
                withSonarQubeEnv('SONARQUBE'){
                    sh "mvn clean package sonar:sonar -D.sonar.organization=ismailahm09 -D.sonar.ProjectKey=ismailahm09"
                }
            }
        }
        stage('Build'){
            steps{
                rtMavenRun (
                    tool: "MVN", // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MVN_DEPLOYER"
                )
            }
        }
         stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JFROG_INSTANCE"
                )
            }
        }
    }
}