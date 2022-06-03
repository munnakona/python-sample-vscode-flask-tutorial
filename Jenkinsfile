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
            checkout(
                giturl: 'https://github.com/munnakona/python-sample-vscode-flask-tutorial.git',
                branch: 'master'
            )
        }
    }

    stage('Setup') { // Install any dependencies you need to perform testing
      steps {
        script {
          sh """
          pip install -r requirements.txt
          """
        }
      }
    }
    stage('Linting') { // Run pylint against your code
      steps {
        script {
          sh """
          pylint **/*.py
          """
        }
      }
    }
    stage('Unit Testing') { // Perform unit testing
      steps {
        script {
          sh """
          python -m unittest discover -s tests/unit
          """
        }
      }
    }
}
