pipeline{
    agent{label 'OPENJDK-1'}
    stages{
        stage('VCS'){
            steps{
<<<<<<< HEAD
                git branch: 'main, url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
=======
                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
>>>>>>> 9318f1f (Commit 1)
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