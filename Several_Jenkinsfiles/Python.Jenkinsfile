pipeline {
    agent {
        label('python')
    }
    stages {
        stage('Is there any python?') {
            steps {
                sh 'python --version'
            }
        }
    }
}