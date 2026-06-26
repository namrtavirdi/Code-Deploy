pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Local Server') {
            steps {
                script {
                    def branch = env.GIT_BRANCH.tokenize('/').last()

                    bat """
                    if not exist "C:\\Deploy\\${branch}" mkdir "C:\\Deploy\\${branch}"

                    xcopy /E /I /Y * "C:\\Deploy\\${branch}\\"
                    """
                }
            }
        }

        stage('Verify') {
            steps {
                bat 'dir C:\\Deploy'
            }
        }
    }
}
