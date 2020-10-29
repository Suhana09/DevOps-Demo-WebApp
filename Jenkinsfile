node{
  stage('SCM'){
    git 'https://github.com/PradeepJagannathan/DevOps-Demo-WebApp'
  }
  stage('compile'){
    def mnvHome = tool name: 'maven', type: maven
    withEnv(["PATH+MAVEn=${tool mvn_version}/bin"]){
      sh 'mvn package'
    }
  }
//  stage ('static code analysis'){
//    def mnvHome = tool name: 'maven', type: maven
//    withSonarQubeEnv('sonarqube'){
//      sh "${mvnHome}/bin/mvn sonar:sonar"
//    }
//  }
}
    
