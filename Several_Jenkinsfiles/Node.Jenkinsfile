pipeline {
    agent {
        label('node')
    }
    stages {
        stage('Is there any node?') {
            steps {
                sh 'node --version'
            }
        }
    }
}