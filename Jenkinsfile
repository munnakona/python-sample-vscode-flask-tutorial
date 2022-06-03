pipeline {
    agent { label 'npm' }
    options {
        timeout(time:1, unit: 'HOURS')
    }
    triggers{
        cron('0 * * * *')
    }
    stages{
        stage('Source Code') {
            steps {
                git url: 'https://github.com/munnakona/python-sample-vscode-flask-tutorial.git',
                branch: 'master'
            }
        }
        stage('Installing packages') {
            steps {
                script {
                    sh 'pip -r requirements.txt'
                }
            }
        }
        }
        stage('Running Unit tests') {
            steps {
                script {
                    sh 'python3.8.10 manage.py test --keepdb --with-xunit --xunit-file=pyunit.xml --cover-xml --cover-xml-file=cov.xml tests/*.py || true'
                    step([$class: 'CoberturaPublisher', 
                        coberturaReportFile: "cov.xml",
                    ])
                    junit "pyunit.xml"
                }
            }
    }
}
