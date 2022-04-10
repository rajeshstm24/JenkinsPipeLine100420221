pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/rajeshstm24/WebApp.git', branch: 'master')
        script {
          try{
            bat 'start /min stopApp.bat'
          }catch(Exception e){
            echo 'nothing running on 9002'
          }
        }

        bat 'mvn install'
        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
      }
    }

    stage('QA UI Automation') {
      parallel {
        stage('QA UI Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppUiAutomation.git', branch: 'master')
            sleep 5
            bat 'mvn test'
          }
        }

        stage('QA API Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppApiAutomation.git', branch: 'master')
            sleep 5
            bat 'mvn test'
          }
        }

      }
    }

    stage('UAT') {
      steps {
        echo 'UAT deployment done'
      }
    }

  }
}