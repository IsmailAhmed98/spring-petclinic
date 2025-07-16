pipeline{
    agent any
    
    stages{
        stage('clone'){
            steps {
                git branch: 'main', url: 'https://github.com/IsmailAhmed98/spring-petclinic.git'
            }
        }
        stage('Sonar'){
            steps {
                withSonarQubeEnv(credentialsId: 'SONAR', installationName: 'SONARQUBE') {
                    sh '''
                     mvn clean package sonar:sonar \
                    -Dsonar.organization=ismailahmed \
                    -Dsonar.projectKey=ismailahmed_spring-petclinic
                    '''
                }
            }
        }
        stage("Docker build"){
            steps {
                withDockerRegistry(credentialsId: 'Docker-ID', url: "https://index.docker.io/v1/") 
                {
                        sh '''
                        docker build -t ismailahmed09/spring-petclinic:1.0 .
                        docker push ismailahmed09/spring-petclinic:1.0
                        docker run -d -p 8081:8081 ismailahmed09/spring-petclinic:1.0
                        '''
                }
            }
        }
    }
}
