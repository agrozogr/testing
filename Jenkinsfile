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
        stage('add test and Timestamp') {
            steps {
                    sh '''date_current=$(date "+%F-%H-%M-%S")
                    echo "$date_current PRjob executed" >> buildlog.txt'''
                }
            }
        stage ('JOBLOG NEW') {
                    agent any
                    steps {
                        echo 'Hello, '

                        sh '''#!/bin/bash
        echo "Hello from jenkins Job, Testing Logs and job info"
        echo "Jobe Name = ${JOB_NAME}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Jobe BUILD_TAG = ${BUILD_TAG}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Jobe BUILD_ID = ${BUILD_ID}" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Jobe Started_by_user= $(cat ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log.txt | grep "Started by user")" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "Full Job logs= $(cat ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log.txt)" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        echo "*************************************** Job info has been write to ${WORKSPACE}/${BUILD_NUMBER}-log.txt ************************"
        echo "************* JOB INFO IS *********************************"
        date_current=$(date "+%F-%H-%M-%S")
        echo "$date_current PRjob executed" >> ${WORKSPACE}/${BUILD_NUMBER}-log.txt
        cat ${WORKSPACE}/${BUILD_NUMBER}-log.txt
                        '''
                    }
                }
    }
}
