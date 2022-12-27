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

    post {
        cleanup {
             dir('${workspace}') {
               def files = findFiles()

               files.each{ f ->
                  if(f.directory) {
                    echo "This is directory: ${f.name} "
                  }
               }
             }
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