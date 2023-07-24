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
                            url: "git@github.com:agrozogr/testing.git",
                            branch: "main",
                            changelog: true,
                            poll: true
                            credentialsId: 'ssh'
                        )
                    }
                }
    }
}

