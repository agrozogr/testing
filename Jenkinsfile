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
        stage('create buildlog.txt file') {
            agent any
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
//        stage('add test and Timestamp') {
//            steps {
//                    sh '''date_current=$(date "+%F-%H-%M-%S")
//                    echo "$date_current PRjob executed" >> buildlog.txt'''
//                }
//            }
        stage ('JOBLOG NEW') {
                    agent any
                    steps {
                        echo '====================== Well, JUST DO IT! '
                        sh '''#!/bin/bash
        echo "====================== Hello from jenkins job, Morty. I did some shitty pipelines, so just check it! "
        echo "Job Name = ${JOB_NAME}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job BUILD_TAG = ${BUILD_TAG}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job BUILD_ID = ${BUILD_ID}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Job Started_by_user= $(cat buildlog.txt | grep "Started by user")" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Full Job logs= $(cat buildlog.txt)" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "====================== Job info has been write to ${WORKSPACE}/${BUILD_NUMBER}-log.txt "
        echo "====================== JOB INFO IS "
        date_current=$(date "+%F-%H-%M-%S")
        echo "====================== $date_current PRjob executed " >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        cat ${WORKSPACE}/${BUILD_NUMBER}-log.txt
                        '''
                    }
                }
    }
}
