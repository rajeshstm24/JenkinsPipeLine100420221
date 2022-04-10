pipeline {
  agent any
  stages {
    stage('Dev Build') {
      steps {
        git(url: 'https://github.com/rajeshstm24/JenkinsPipeLine100420221.git', branch: 'master', poll: true)
        script {
          try{
            bat 'start /min stopApp.bat'
          }catch(Exception e){
            echo 'Nothing running on 9002'
          }
        }

        bat 'mvn install'
        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
      }
    }

    stage('QA Test') {
      parallel {
        stage('QA Test') {
          steps {
            echo 'QA UI Automation'
          }
        }

        stage('QA API Automation') {
          steps {
            echo 'QA API Automation'
          }
        }

      }
    }

    stage('UAT') {
      steps {
        echo 'UAT Done'
      }
    }

    stage('Prod') {
      steps {
        input 'Can I deploy to Prod'
      }
    }

  }
}