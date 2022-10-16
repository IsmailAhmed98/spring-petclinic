pipeline{
    agent{label 'OPENJDK-1'}
    stages{
        stage('VCS'){
            steps{
                git branch: 'main, url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('Build'){
            steps{
                sh 'maven package'
            }
        }
        stage('Artifactory'){
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}