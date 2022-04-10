pipeline {
  agent any
  stages {
    stage('Dev Build') {
      steps {
        echo 'Dev Done'
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