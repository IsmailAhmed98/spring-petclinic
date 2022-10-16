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
                sh 'maven package'
            }
        }
        stage('Artifactory'){
            steps{
                    archiveArtifacts artifacts: 'target/*.jar'
            }
            
        }
    }
}