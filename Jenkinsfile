pipeline{
    agent{label 'OPENJDK_1'}
    stages{
        stage('VCS'){
            steps{


                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'

            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Artifactory'){
            steps{
                    archiveArtifacts artifacts: 'target/*.jar'
            }
            
        }
        stage('Artifactory Config'){
            steps{
                rtMavenDeployer(
                    id:"Maven_Deployer",
                    serverId:"JFROG-ID",
                    releaseRepo:"prac-libs-release-local",
                    snapshotRepo:"prac-libs-snapshot-local"
                )
            } 
        }
        stage('execute maven'){
            steps{
                rtMavenRun(
                    tool:'MVN',
                    pom:'pom.xml',
                    goals:'clean package',
                    deployerId:"Maven_Deployer"
                )
            }
        }
    }
    post{
        always{
            mail subject: 'Build completed',
                 body: 'Build has been completed',
                 to: 'ismailahmed@gmail.com'
        }
    }
}