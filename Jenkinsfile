pipeline{
    agent{label 'Node2'}
    stages{
        stage( 'source code from git' ){
            steps{
               git branch : 'master',
               url: 'https://github.com/munnakona/python-sample-vscode-flask-tutorial.git'
            }
        }
        stage('build'){
            steps{
                sh 'pip install -r requirements.txt'
            }
        }
        stage('test'){
            steps{
                sh 'pip install pytest pytest-azurepipelines'
                sh 'pip install pytest-cov'
                sh 'pytest --doctest-modules --junitxml=junit/test-results.xml --cov=. --cov-report=xml'
            }
        }
        stage( 'publish'){
            steps{
                junit testResults: '**/test-*.xml'
            }
        }
    }
}