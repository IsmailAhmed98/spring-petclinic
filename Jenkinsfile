pipeline{
    stages{
        stage('Clone'){
            step{
                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('build'){
            step{
                sh '/opt/apache-maven-3.9.4/bin/mvn package'
            }
        }
        stage('archive tests'){
            step{
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('archive results'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }
}