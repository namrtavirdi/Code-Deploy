pipeline {
    agent any

    stages {

        stage('Clone Source') {
            steps {
                echo 'Repository cloned by Jenkins.'
            }
        }

        stage('Deploy to Local Server') {
            steps {
                bat '''
                if not exist "C:\\Deploy" mkdir "C:\\Deploy"
                xcopy /E /I /Y * "C:\\Deploy\\"
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'dir C:\\Deploy'
            }
        }
    }
}
