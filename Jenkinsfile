pipeline {
    agent {
        docker { image 'python:3.11-slim' }
    }
    stages {
        stage('Install dependencies') {
            steps {
                sh '''
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest --maxfail=1 --disable-warnings -q --junitxml=test-results.xml'
            }
        }

        stage('Archive Results') {
            steps {
                junit 'test-results.xml'
            }
        }
    }

    triggers {
        pollSCM('* * * * *')
    }
}
