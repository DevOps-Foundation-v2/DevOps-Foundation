pipeline {
    agent any 
    environment {
       DOCKER = tool 'docker' 
       DOCKER_EXEC = '$DOCKER/docker'
       transitionInput = "[transition:[id:'5']]"
    }
    stages {
      
      stage('SCM') {
         steps {
            figlet 'SOURCE-CONTROL-MANAGEMENT'
            checkout scm // clonacion de codigo en nodo
         }
      }
        
       stage('JIRA') {
         steps {
             withEnv(['JIRA_SITE=https://fundamentosdevops.atlassian.net']) {
                jiraTransitionIssue idOrKey: 'DF-1', input: env.transitionInput
             }
         }
      }
        
      stage('BUILD') {
         steps {
            figlet 'BUILD'
            sh 'set +x; chmod 777 mvnw'
            sh './mvnw clean install'
          //archiveArtifacts artifacts: "build/libs/testing-web-*.jar"
         }
      }
        
      stage('SAST') {
         steps {
            withCredentials([string(credentialsId: 'sonarcloud', variable: 'SONARPAT')]) {
                 figlet 'SAST-SONARCLOUD'
                 //sh('set +x; ./gradlew sonarqube -Dsonar.login=$SONARPAT -Dsonar.branch.name=feature-jenkins')
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
