pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy Based on Branch') {
            steps {
                script {

                    def branch = env.GIT_BRANCH ?: ''
                    def deployPath = ""

                    echo "Current Branch: ${branch}"

                    if (branch.contains('main')) {
                        deployPath = "C:\\inetpub\\wwwroot\\main"
                    }
                    else if (branch.contains('dev')) {
                        deployPath = "C:\\inetpub\\wwwroot\\dev"
                    }
                    else {
                        error("Branch not configured.")
                    }

                    bat """
                    if not exist "${deployPath}" mkdir "${deployPath}"
                    xcopy * "${deployPath}\\" /E /I /Y
                    """
                }
            }
        }

        stage('Display Branch Content') {
            steps {
                script {

                    def branch = env.GIT_BRANCH ?: ''

                    if (branch.contains('main')) {

                        bat '''
                        echo ===== MAIN BRANCH =====
                        type C:\\inetpub\\wwwroot\\main\\index.html
                        '''

                    } else if (branch.contains('dev')) {

                        bat '''
                        echo ===== DEV BRANCH =====
                        type C:\\inetpub\\wwwroot\\dev\\index.html
                        '''

                    }
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
