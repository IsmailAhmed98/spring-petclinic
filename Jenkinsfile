pipeline{
    agent {label 'ubuntu'}
    tools {maven 'MAVEN_HOME'}
    parameters { choice(name: 'BUILD', choices: ['package', 'clean'], description: 'The build command') }
    triggers { pollSCM('* * * * *') }
    stages{
        stage('Clone'){
            steps{
                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn ${params.BUILD}'
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