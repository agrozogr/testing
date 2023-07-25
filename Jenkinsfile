pipeline {
    agent any
    stages {
        stage("Clone Git Repository") {
            steps {
                git(
                    url: "https://github.com/agrozogr/testing.git",
                    branch: "main",
                    changelog: true,
                    poll: true,
                    credentialsId: 'github_access_token4'
                )
            }
        }
        stage ('JOB LOG INGO') {
                    agent any
                    steps {
                        echo '====================== Well, JUST DO IT! '
                        sh '''#!/bin/bash
        echo "====================== Hello from jenkins job, Morty. I did some shitty pipelines, so just check it! "
        echo "Job Name = ${JOB_NAME}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job BUILD_TAG = ${BUILD_TAG}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job BUILD_ID = ${BUILD_ID}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job Started_by_user= $(cat buildlog.txt | grep "Started by user")" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "====================== Full Job logs: "
        echo "$(cat job.log)" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "====================== Job info has been write to ${WORKSPACE}/${BUILD_NUMBER}-log.txt "
        echo "====================== JOB INFO IS "
        date_current=$(date "+%F-%H-%M-%S")
        echo "====================== $date_current PRjob executed " >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        cat ${WORKSPACE}/${BUILD_NUMBER}-log.txt
                        '''
                    }
                }
        stage("====================== COPY new file job log to GitHub repo") {
                    steps {
                    sh "cd ${WORKSPACE}"
                    sh "git add job.log"
                    sh "git commit -m 'Add job.log file from Jenkins Pipeline'"
                    }
                }
        stage("====================== Push to Git Repo") {
                    steps {
                        withCredentials([gitUsernamePassword(credentialsId: 'github_access_token4', gitToolName: 'Default')]) {
                        sh "git push -u origin main"
                    }
                    }
                }
    }
}
