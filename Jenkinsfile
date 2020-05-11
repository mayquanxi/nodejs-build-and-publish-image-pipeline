pipeline {
   agent none
   triggers {
      pollSCM('*/2 * * * *')
   }
   stages {
      stage('Build image in Sequential') {
        agent {
          docker {
            image 'node:13'
            args '-d -p 3000:3000 --name nodejs-building'
          }
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
      stage('Push image') {
         agent {
            node {
               label 'master'
            }
         }
         stages {
            stage('tag and push image){
               steps {
                  sh 'docker commit nodejs-building nodejs-building'
                  sh 'docker tag $(docker images nodejs-building -qa) mayquanxi/nodejs'
                  sh 'docker push mayquanxi/nodejs'
               }
            }
         }
      }
   }
} 
