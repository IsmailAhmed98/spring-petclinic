pipeline{
    agent {label 'ubuntu'}
    tools {maven 'MAVEN_HOME'}
    parameters { choice(name: 'BUILD', choices: ['package', 'clean'], description: 'The build command') 
                 choice(name: 'BRANCH', choices: ['main', 'Ismail'], description: 'The branch to use')}
    triggers { pollSCM('* * * * *') }
    stages{
        stage('Clone'){
            steps{
                git branch: "${params.BRANCH}", url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh "mvn ${params.BUILD}"
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