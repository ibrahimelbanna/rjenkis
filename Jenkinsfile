pipeline {

        agent {

        label 'master'

           }

	options {
	
	  buildDiscarder (logRotator(numToKeepStr:'2',artifactNumToKeepStr: '1'))

          }

        stages {

        stage('Unit Tests'){
            steps {
                echo 'hello world'
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


