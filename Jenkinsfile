pipeline {
    agent any 
    environment {
       DOCKER = tool 'docker' 
       DOCKER_EXEC = '$DOCKER/docker'
       SCA = '/Users/clagosu/Documents/dependency-check/bin/dependency-check.sh'
    }
    stages {
      
      stage('SCM') {
         steps {
            figlet 'SOURCE-CONTROL-MANAGEMENT'
            checkout scm // clonacion de codigo en nodo
         }
      }
        
      stage('BUILD') {
         steps {
            figlet 'BUILD'
            sh 'set +x; chmod 777 gradlew'
            sh './gradlew clean build'
          //archiveArtifacts artifacts: "build/libs/testing-web-*.jar"
         }
      }
        
      stage('SAST') {
         steps {
            withCredentials([string(credentialsId: 'sonarcloud', variable: 'SONARPAT')]) {
                 figlet 'SAST-SONARCLOUD'
                 sh('set +x; ./gradlew sonarqube -Dsonar.login=$SONARPAT -Dsonar.branch.name=feature-jenkins')
            }
         }
      }
        
 
        
      stage('Build Image') {
         steps {
            figlet 'IMAGE'
          //sh '${DOCKER EXEC} build .'
            //sh "$DOCKER_EXEC images"
          //sh "$DOCKER_EXEC push clagosu/spring-clinic:$currentBuild.number"
            }
        }
        
   }
}
