pipeline {
  agent any
  tools {
    maven 'maven'
  }
  
  stages {
    stage('SCM'){
      steps {
        git 'https://github.com/PradeepJagannathan/DevOps-Demo-WebApp'
      }
    }
    stage('compile'){
      steps {
 //       def mvnHome = tool name: 'maven', type: maven
        sh "mvn compile"
      }
    }
    stage ('static code analysis') {
      steps {
        withSonarQubeEnv ('SonarQube Scanner') {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
    stage("Quality Gate") {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  //  stage ('static code analysis'){
  //    def mnvHome = tool name: 'maven', type: maven
  //    withSonarQubeEnv('sonarqube'){
  //      sh "${mvnHome}/bin/mvn sonar:sonar"
  //    }
  //  }
  }
}
    
