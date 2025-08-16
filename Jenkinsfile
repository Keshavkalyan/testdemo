pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q --junitxml=test-results.xml
                '''
            }
        }

        stage('Archive Results') {
            steps {
                junit 'test-results.xml'
            }
        }
    }

    triggers {
        pollSCM('* * * * *')  // every 1 min check repo
    }
}
