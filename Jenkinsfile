stage('Deploy to Local Server') {
    steps {
        script {
            def branch = env.GIT_BRANCH.tokenize('/').last()
            def deployPath = "C:\\inetpub\\wwwroot\\${branch}"

            bat """
            if not exist "${deployPath}" mkdir "${deployPath}"
            xcopy /E /I /Y * "${deployPath}\\"
            """
        }
    }
}
