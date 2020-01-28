#!/usr/bin/env groovy
pipeline {

        agent {

        label 'master'

           }
   environment {
      PROJECT_NAME = 'biohome-R-Prject'
      APP_VERSION = "0.1.${env.BUILD_NUMBER}"
  }


	options {
	
	   buildDiscarder(logRotator(numToKeepStr: '10', daysToKeepStr: '5', artifactNumToKeepStr: '10', artifactDaysToKeepStr: '5'))
      timeout(time: 100, unit: 'MINUTES')
      disableConcurrentBuilds()

          }

        stages {
        stage('Set Env Variables') {
            steps {
                setEnvVariables()
                echo "${env.CURRENT_ENV}"
                echo "${env.GIT_BRANCH}"
              }
            
         }
        stage('Unit Tests'){
            steps {
                echo 'hello world'
                sh "printenv"
                echo "${env.BUILD_ID}"
                echo "${env.BUILD_ID}"
              }

         }
        stage('build'){

           steps {
                sh 'R CMD build .'
                sh 'printenv'
                 }
             }
        stage('backup'){
           steps {
              echo 'Do backuping here'
            }

        }
          
        stage('deploy'){
          steps {
             echo 'Do deployment here'
           }

        }
        stage('Coverage'){
            steps {
                sh '''
                  app_lines=`cat app.sh | wc -l`
                  cov_lines=`cat ${BUILD_ID}.cov | wc -l`
                  echo The app has `expr $app_lines - $cov_lines` lines uncovered > ${BUILD_ID}.rpt
                  cat ${BUILD_ID}.rpt
                '''
                archiveArtifacts "${env.BUILD_ID}.rpt"
            }
        }      

         
	post {

	    always {
		      archiveArtifacts artifacts: "*.tar.gz"

        }
        }   
  }

def stagesMap() {
  return [
    'develop': 'dev',
    'test': 'test',
    'stage': 'stage',
    'master': 'prod'
  ]
}

def setEnvVariables() {
  env.CURRENT_ENV = stagesMap().get(env.GIT_BRANCH.toString().split("/")[1])
  echo '${env.CURRENT_ENV}'
}
