pipeline{
    agent {label "OPENJDK-11"}
    
    stages{
        stage('VCS'){
            steps{
                git branch:'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Archives'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
        stage('test'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
        
    }
}
