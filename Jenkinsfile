pipeline {

        agent {

        label 'master'

           }
   environment {
      PROJECT_NAME = 'biohome-R-Prject'
      APP_VERSION = "0.1.${env.BUILD_NUMBER}"
  }


	options {
	
	  buildDiscarder (logRotator(numToKeepStr:'2',artifactNumToKeepStr: '1'))

          }

        stages {
        stage('Set Env Variables') {
            steps {
                setEnvVariables()
              }
            echo "${env.CURRENT_ENV}"
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
           
        }

         
	post {

	    always {
    echo 'Build Number'
    echo '${env.BUILD_NUMBER}'
		archiveArtifacts  artifacts: '*.tar.gz' , fingerprint: true

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
  env.CURRENT_ENV = stagesMap().get(env.GIT_BRANCH)
}
