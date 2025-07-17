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
                        sh 'docker build -t ismailahmed09/spring-petclinic:1.0 .
                        '
                }
            }
        }
        stage("Trivy test"){
            steps {
                sh 'trivy image ismailahmed09/spring-petclinic:1.0'
            }
        }
        stage("Docker push"){
            steps {
                sh ' docker push ismailahmed09/spring-petclinic:1.0'      
            }
        }
        stage("K8s Deploy"){
            steps {
                withCredentials([file(credentialsId: 'Kube-Config', variable: 'KUBECONFIG')]) {
                        sh '''
                            kubectl apply -f deployment.yaml
                            kubectl apply -f service.yaml
                            '''
                }
            }
        }
    }
}
