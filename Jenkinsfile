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

    stage('QA UI Automation') {
      parallel {
        stage('QA UI Automation') {
          steps {
            ws(dir: 'workspace/WebAppUiAutomation') {
              git(url: 'https://github.com/rajeshstm24/WebAppUiAutomation.git', branch: 'master')
              sleep 5
              bat 'mvn test'
            }

          }
        }

        stage('QA API Automation') {
          steps {
            ws(dir: 'workspace/WebAppApiAutomation') {
              git(url: 'https://github.com/rajeshstm24/WebAppApiAutomation.git', branch: 'master')
              sleep 5
              bat 'mvn test'
            }

          }
        }

      }
    }

    stage('UAT') {
      steps {
        echo 'UAT Done'
      }
    }

  }
}