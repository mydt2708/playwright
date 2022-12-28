pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
                bat "%ANT_HOME%/bin/ant.bat clean compile"
                currentBuild.name = "MY_VERSION_NUMBER"
                currentBuild.description = "MY_PROJECT MY_VERSION_NUMBER"
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