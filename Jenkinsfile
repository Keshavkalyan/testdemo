pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest --maxfail=1 --disable-warnings -q'
            }
        }

        stage('Archive Results') {
            steps {
                junit '**/test-results.xml'
            }
        }
    }

    triggers {
        pollSCM('* * * * *')  // every 1 min check repo
    }
}

