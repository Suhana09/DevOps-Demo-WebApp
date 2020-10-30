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
//    stage ('static code analysis') {
//      steps {
//        withSonarQubeEnv ('sonarqube') {
//          sh 'mvn clean package sonar:sonar \
//          -Dsonar.sources=. 
//        }
//      }
//    }
    stage ('Code Analysis') {
      steps {
        script {
          def scannerHome = tool 'SonarQube Scanner';
          withSonarQubeEnv(credentialsId: 'sonar-webhook') {
            sh "${tool("SonarQube Scanner")}/bin/sonar-scanner \
            -Dsonar.sources=. \
            -Dsonar.tests=. \
            -Dsonar.inclusions=**/test/java/servlet/createpage_junit.java \
            -Dsonar.test.exclusions=**/test/java/servlet/createpage_junit.java \
            -Dsonar.login=admin \
            -Dsonar.password=admin"   
          }
        }
      }
    }
      
    stage("Quality Gate") {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate webhookSecretId: 'sonarwebhook'
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
    
