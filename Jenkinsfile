pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage("Clone Git Repository") {
                    steps {
                        git(
                            url: "https://github.com/agrozogr/testing",
                            branch: "main",
                            changelog: true,
                            poll: true
                        )
                    }
                }
    }
}

