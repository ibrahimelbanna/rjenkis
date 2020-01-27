pipeline {

        agent {

        label 'master'

           }
   environment {
      PROJECT_NAME = 'biohome-R-Prject'
      APP_VERSION = "0.1.${env.BUILD_NUMBER}"
  }

    parameters
  {
    choice(name: 'ENVIRONMENT', choices: ['DEV_TO_TEST', 'TEST_TO_STAGE', 'STAGE_TO_PROD'], description: 'Git merge type')
    choice(name: 'COMPONENT', choices: ['Lambda_DataWatch','Lambda_Workslate','Lambda_Dashboard','Lambda_CustomViews','Lambda_DataSync','Lambda_Notes','Lambda_Layers','API','Frontend'], description: 'Component we want to deploy')
    choice(name: 'VERSION', choices: ['V2','V1'], description: 'Component version')
  }


	options {
	
	  buildDiscarder (logRotator(numToKeepStr:'2',artifactNumToKeepStr: '1'))

          }

        stages {

        stage('Unit Tests'){
            steps {
                echo 'hello world'
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
    echo '$BUILD_NUMBER'
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
  env.CURRENT_ENV = stagesMap().get(BRANCH_NAME)
}
