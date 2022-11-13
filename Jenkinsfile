pipeline {
    agent any

    stages {
         stage('Cloning from GitHub') {
                steps {
                    git branch: 'marouen', url: 'https://github.com/mariemgharbi14/devops5nids.git'
                }  
            }
        
        stage('MVN CLEAN') {
                steps {
                     sh 'mvn clean '
                }
            }
              
          stage('MVN COMPILE') {
            steps {
               sh 'mvn compile'
           }
        }
          stage('mvn Test') {
            steps {
               sh 'mvn test'
            }
        }
          stage('mvn Verify') {
             steps {
               sh 'mvn verify'
          }
       }
         stage ('Scan Sonar'){
            steps {
    sh "mvn sonar:sonar \
  -Dsonar.projectKey=sonar2 \
  -Dsonar.host.url=http://192.168.1.77:9000 \
  -Dsonar.login=32039c22e8427fa69fe20432170dc89eaef912ac -DskipTests"
    }
        }
        stage('Nexus') {
      steps {
        sh 'mvn clean deploy -Dmaven.test.skip=true'
      }
    }
    }
    
    post {
                success {
                   echo 'succes'
                }
failure {
                  echo 'failed'   
                }
             
       
    }

}