pipeline{
    agent {label 'ubuntu'}
    tools {maven 'MAVEN_HOME'}
    parameters{choice(name: 'Branch', choices:['main', 'Ismail'], description: 'The branch to use')
                choice(name:' Build', choices:['package','clean'], description: 'The build command is')}
    triggers{pollSCM('* * * * *')}
    stages{
        stage('Clone'){
            steps{
                git branch: "${params.Branch}", url: 'git@github.com:IsmailAhmed98/spring-petclinic.git'
                mail subject: 'Started',
                    body: "The build has begun for build name $env.JOB_NAME and ID $env.BUILD_ID"

            }
        }
        stage('Build'){
            steps{
                mvn "${params.Build}"
            }
        }
    }
    post{
        always{
            mail subject: 'Completed',
                body: "The build has been completed for build name $env.JOB_NAME and ID $env.BUILD_ID"
        }
        failure{
            mail subject: 'Failure',
                body:"The build has failed for build name $env.JOB_NAME and ID $env.BUILD_ID"
        }
        success{
            mail subject: 'Successful',
                body: "The build was a success for build name $env.JOB_NAME and ID $env.BUILD_ID"
                junit 'target/surefire-reports/*.xml'
        }
    }
}
