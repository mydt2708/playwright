pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
                script {
                    currentBuild.displayName = "The name."
                    currentBuild.description = "The best description."
                }
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