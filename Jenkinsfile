pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to IIS') {
            steps {
                script {

                    // Get the current branch name
                    def branch = env.GIT_BRANCH.tokenize('/').last()

                    // IIS deployment path
                    def deployPath = "C:\\inetpub\\wwwroot\\${branch}"

                    bat """
                    if not exist "${deployPath}" mkdir "${deployPath}"
                    xcopy * "${deployPath}\\" /E /I /Y
                    """
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    def branch = env.GIT_BRANCH.tokenize('/').last()

                    bat """
                    echo ==========================
                    echo Deployment Successful
                    echo Branch : ${branch}
                    echo Folder : C:\\inetpub\\wwwroot\\${branch}
                    echo ==========================

                    dir C:\\inetpub\\wwwroot\\${branch}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully!"
        }

        failure {
            echo "Deployment failed!"
        }
    }
}
