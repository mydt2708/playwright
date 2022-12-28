pipeline {
    agent any


    parameters {
        string(name: 'TEST_FILE_OR_FOLDER', defaultValue: './examples/basic/login_and_verify.spec.ts', description: 'Testing directory')
        string(name: 'SHARDS', defaultValue: '1', description: 'How many shards should we use?')
        string(name: 'SUITE_ID_OR_CASE_ID', defaultValue: 'TC_SB_DB_LGIN_001', description: 'The Tag, Suite or Case ID that need to run. If empty --> run all tests from TEST_FILE_OR_FOLDER')
        string(name: 'CI_ENV', defaultValue: 'dev', description: 'Which env to perform tests?')
        string(name: 'BRANCH', defaultValue: 'master', description: 'Which code branch to perform tests?')
        string(name: 'TH_JOB_ID', defaultValue: '-1', description: 'Testhub Job ID (If run directly, please skip it)')
        string(name: 'SLACK_ID', defaultValue: '', description: 'Your slack ID to get notification')
        string(name: 'TH_JOB_NAME', defaultValue: '', description: 'Testhub Job Name')
        string(name: 'TH_JOB_RUN_MODE', defaultValue: '', description: 'Testhub Run mode (one-time|multiple-time)')
    }


    stages {
        stage('Set description') {
            steps {
                script {
                currentBuild.displayName = "[${CI_ENV}]_[${BRANCH}]_[${SUITE_ID_OR_CASE_ID}]"
                currentBuild.description = "${TH_JOB_NAME}"
                }
            }
        }
        stage('Build') {
            steps {
                echo "Building application..."
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }

    post {
        cleanup {
            sh "ls ${workspace}"
            /* clean up our workspace */
            deleteDir()
            /* clean up tmp directory */
            dir("${workspace}@tmp") {
                deleteDir()
            }
            /* clean up script directory */
            dir("${workspace}@script") {
                deleteDir()
            }
            sh "ls ${workspace}"
        }
    }
}