pipeline {
  agent any
  stages {
    stage('SCM'){
      steps {
        git 'https://github.com/PradeepJagannathan/DevOps-Demo-WebApp'
      }
    }
    stage('compile'){
      steps {
        def mvnHome = tool name: 'maven', type: maven
        sh "${mvnHome}/bin/mvn compile"
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
    
