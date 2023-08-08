pipeline{
    agent any
    tools {maven 'MAVEN_HOME'}
    parameters{choice(name: 'Branch', choices:['main', 'Ismail'], description: 'The branch to use')
                choice(name:' Build', choices:['clean install','package'], description: 'The build command is')}
    triggers{pollSCM('* * * * *')}
    stages{
        stage('Clone'){
            steps{
                git branch: "${params.Branch}", url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
                mail subject: 'Started',
                    body: "The build has begun for build name $env.JOB_NAME and ID $env.BUILD_ID",
                    to : 'ismail@gmail.com'

            }
        }
        stage ('Artifactory configuration') {
            steps {
               // rtServer (
                  //  id: "JFROG_INSTANCE",
                  //  url: 'https://ismailahm.jfrog.io/',
                  //  credentialsId: "CRED_ID"
               // )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "JFROG_INSTANCE",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "JFROG_INSTANCE",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: MAVEN_HOME, // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: "${params.Build}",
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
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
    post{
        always{
            mail subject: 'Completed',
                body: "The build has been completed for build name $env.JOB_NAME and ID $env.BUILD_ID",
                to: 'ismail@gmail.com'
        }
        failure{
            mail subject: 'Failure',
                body:"The build has failed for build name $env.JOB_NAME and ID $env.BUILD_ID",
                to: 'ismail@gmail.com'
        }
        success{
            mail subject: 'Successful',
                body: "The build was a success for build name $env.JOB_NAME and ID $env.BUILD_ID",
                to: 'ismail@gmail.com'
                junit 'target/surefire-reports/*.xml'
        }
    }
}

