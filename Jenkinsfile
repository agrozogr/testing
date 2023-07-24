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
                    poll: true,
                    credentialsId: 'ssh'
                )
            }
        }
        stage('create job.log file') {
            steps {
                script {
                    def logContent = Jenkins.getInstance()
                        .getItemByFullName(env.JOB_NAME)
                        .getBuildByNumber(
                            Integer.parseInt(env.BUILD_NUMBER))
                        .logFile.text
                    // copy the log in the job's own workspace
                    writeFile file: "buildlog.txt", text: logContent
                }
            }
        }
    }
}
