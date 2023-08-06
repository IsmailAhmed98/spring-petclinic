pipeline{
    stages{
        stage('Clone'){
            steps{
                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh '/opt/apache-maven-3.9.4/bin/mvn package'
            }
        }
        stage('archive tests'){
            steps{
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