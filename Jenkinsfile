pipeline {
    agent { label 'npm' }
    options {
        timeout(time:1, unit: 'HOURS')
    }
    triggers{
        cron('0 * * * *')
    }
    stages {
          stage('Checkout code') {
        steps {
            checkout scm
        }
    }
    stage('build') {
      steps {
        sh 'pip install -r requirements.txt'
      }
    }
    stage('test') {
      steps {
        sh 'python test_test1.py'
      }
      post {
        always {
          junit 'test-reports/*.xml'
        }
      }    
    }
  }
}
