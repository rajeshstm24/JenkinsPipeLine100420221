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
        stage('QA UI Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppUiAutomation.git', branch: 'master', poll: true)
            sleep 5
            bat 'mvn test'
          }
        }

        stage('QA API Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppApiAutomation.git', branch: 'master', poll: true)
            sleep 5
            bat 'mvn test'
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