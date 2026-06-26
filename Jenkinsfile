pipeline {
    agent any

    stages {
        stage('Deploy to Local Server') {
            steps {
                bat '''
                if not exist "C:\\Deploy" mkdir "C:\\Deploy"
                xcopy /E /I /Y * "C:\\Deploy\\"
                '''
            }
        }

        stage('Verify') {
            steps {
                bat 'dir C:\\Deploy'
            }
        }
    }
}