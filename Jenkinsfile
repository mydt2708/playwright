pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
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

    steps {
        script {
                     dir('${workspace}') {
                       def files = findFiles()

                       files.each{ f ->
                          if(f.directory) {
                            echo "This is directory: ${f.name} "
                          }
                       }
                     }
        }
        }
    post {
        cleanup {
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
        }
    }

        steps {
            script {
                         dir('${workspace}') {
                           def files = findFiles()

                           files.each{ f ->
                              if(f.directory) {
                                echo "This is directory: ${f.name} "
                              }
                           }
                         }
            }
            }
}