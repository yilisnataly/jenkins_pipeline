pipeline {
    agent {
        label('python')
    }
    environment {
        PYPI_CREDENTIALS = credentials('pypi-credentials')
    }
    triggers {
            cron('*/2 * * * *')
    }
    options { 
        disableConcurrentBuilds()
            timeout(time: 1, unit: 'MINUTES')
                timestamps()
    }
    stages {
        stage('Build') {
            steps {
                dir('python-application-example') {
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        stage('Unit Test') {
            steps {
                dir('python-application-example') {
                    sh 'python -m coverage run -m pytest -s -v'
                }
            }
        }

        stage('Coverage') {
            steps {
                dir('python-application-example') {
                    sh 'python -m coverage report -m --fail-under=90'
                }
            }
        }

        stage('Package') {
            steps {
                dir('python-application-example') {
                    sh 'python -m build'
                }
            }
        }

        stage('Publish') {
            steps {
                dir('python-application-example') {
                    timeout(time: 10, unit: 'MINUTES') {
                        input message: 'Are you sure to deploy?', ok: 'Yes, deploy to pypi'
                            sh 'python -m twine upload dist/* -u $PYPI_CREDENTIALS_USR -p $PYPI_CREDENTIALS_PSW --skip-existing'
                    } 
                } 
            }
        }
    }
}