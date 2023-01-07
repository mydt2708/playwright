pipeline {
    agent any

    options {
        skipDefaultCheckout true
    }

    parameters {
        string(name: 'TEST_FILE_OR_FOLDER', defaultValue: './tests/demo.spec.ts', description: 'Testing directory')
        string(name: 'SHARDS', defaultValue: '1', description: 'How many shards should we use?')
        string(name: 'SUITE_ID_OR_CASE_ID', defaultValue: 'TC_SB_DB_LGIN_001', description: 'The Tag, Suite or Case ID that need to run. If empty --> run all tests from TEST_FILE_OR_FOLDER')
        string(name: 'CI_ENV', defaultValue: 'dev', description: 'Which env to perform tests?')
        string(name: 'BRANCH', defaultValue: 'main', description: 'Which code branch to perform tests?')
        string(name: 'TH_JOB_ID', defaultValue: '-1', description: 'Testhub Job ID (If run directly, please skip it)')
        string(name: 'SLACK_ID', defaultValue: '', description: 'Your slack ID to get notification')
        string(name: 'TH_JOB_NAME', defaultValue: '', description: 'Testhub Job Name')
        string(name: 'TH_JOB_RUN_MODE', defaultValue: '', description: 'Testhub Run mode (one-time|multiple-time)')
    }


    stages {
        stage('Update job desc') {
            steps {
                script {
                currentBuild.displayName = "${ID()} - ${USER()}"
                if (env.TH_JOB_NAME != null && env.TH_JOB_NAME != "") {
                  currentBuild.description = "${TH_JOB_NAME}"
                  }
                }
            }
        }


        stage('Running tests') {
            steps {
                script {
                        if (SUITE_ID_OR_CASE_ID != null && SUITE_ID_OR_CASE_ID != "") {
                            sh """
                                node -v
                                npm install -g yarn
                                yarn install
                                set +e
                                CI_ENV=${CI_ENV} yarn test ${TEST_FILE_OR_FOLDER} -g "${SUITE_ID_OR_CASE_ID}" --shard=${shardNum}/${SHARDS}
                                set -e
                            """
                        } else {
                            sh """
                                git clone git@github.com:mydt2708/playwright.git
                                yarn install
                                set +e
                                yarn test ${TEST_FILE_OR_FOLDER}
                                set -e
                            """
                        }
                }
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

def USER() {
 wrap([$class: 'BuildUser']) {
      return env.BUILD_USER
    }
}

def ID() {
 wrap([$class: 'BuildUser']) {
      return env.BUILD_DISPLAY_NAME
    }
}
