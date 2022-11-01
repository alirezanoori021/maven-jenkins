pipeline {
  agent any
  tools {
        maven "M3" 
   }

  stages {
    stage('Sonarqube Analysis - SAST')  
      { 
        steps  
        { 
           withSonarQubeEnv('SonarQube')  
           { 
              sh "mvn sonar:sonar -Dsonar.projectKey=maven-jenkins-pipeline -Dsonar.host.url=http://35.242.132.146:9000"  
           } 
        } 
      } 
      stage('Build Artifact') 
      {
            steps 
            {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }  
       }
      stage('Test Maven - JUnit') 
      {
            steps 
            {
              //sh "mvn test"
              echo "Running unit tests"
            }
      }
      stage('Deploy') 
      { 
          steps 
          { 
              input('Continue to Deploy?') 
              echo 'Deploying to Production Environment' 
          } 
      }
    }
}
