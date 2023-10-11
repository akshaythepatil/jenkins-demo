pipeline{
    agent any
    tools{
        maven 'MyMaven'
    }
    stages{
        stage("Build maven project"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/akshaythepatil/jenkins-demo']])
                sh "mvn clean install"
            }
        }
          stage("Build Docker image"){
            steps{
                script{
                   dockerImage= docker.build("akshaythepatil/jenkins-demo")
                }
            }
        }
          stage("push Docker image"){
            steps{
                script{
                    docker.withRegistry('','dockerhub'){
                          dockerImage.push();
                          dockerImage.push('latest');
                    }
                  
                }
            }
        }
    }
    
    
}