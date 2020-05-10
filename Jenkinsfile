pipeline {
        agent {
              docker {
                    image 'node:13'
                    args '-p 3000:3000'
              }
        }
        triggers {
              pollSCM('*/2 * * * *')
        }
        stages {
              stage('build') {
                    steps {
                         echo 'check version nodejs:'
                         sh 'node --version'
                    }
              }
              stage('Test code') {
                    steps {
                         sh 'node ./app.js & sleep 10'
                         input message: 'Finished using the web site? (Click "Proceed" to continue)'        
                    }     
              }
        }
}
