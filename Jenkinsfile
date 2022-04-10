pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        ws(dir: 'workspace/WebApp') {
          git(url: 'https://github.com/rajeshstm24/JenkinsPipeLine100420221.git', branch: 'master')
          script {
            try{
              bat 'start /min stopApp.bat'
            }catch(Exception e){
              echo 'Nothing running on 9002'
            }
          }

          bat 'mvn clean install'
          bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
        }

      }
    }

  }
}