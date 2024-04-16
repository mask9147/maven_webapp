pipeline{
        agent {
                docker {
                image 'maven'
                //args '-v $HOME/.m2:/root/.m2'
                args '-u root'
                }
        }
        stages{
              stage('Sonar Scan'){
                  steps{
                      script{
                      withSonarQubeEnv('sonarserver') { 
                      sh "mvn sonar:sonar"
                       }
		              // sh "mvn clean install"
                  }
                }  
              }
              stage('Maven Build'){
                  steps{
                      script{
		                  sh "mvn clean install"
                  }
                }  
              }
              stage('Deploy'){
                  steps{
                    deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://3.86.91.242:8080/')], contextPath: 'Demo', war: 'target/*war'
                }  
              }
        }
}
