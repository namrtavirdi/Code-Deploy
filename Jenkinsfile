pipeline {
    agent any

    environment {
        DEPLOY_PATH = "C:\\Deploy"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                script {

                    def branch = env.GIT_BRANCH.tokenize('/').last()

                    bat """
                    if not exist "%DEPLOY_PATH%\\${branch}" mkdir "%DEPLOY_PATH%\\${branch}"

                    xcopy * "%DEPLOY_PATH%\\${branch}\\" /E /Y /I
                    """

                    echo "Deployment completed to ${branch}"
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
