pipeline {
  agent any

  stages {
     stage('cleaning') { 
        steps { 
            cleanWs()
        }
    }
    stage('Checkout Scm') {
      steps {
        git 'https://github.com/dipdee/Jenkins-pipeline.git'
      }
    }

    stage('Shell script 0') {
      steps {
        sh '''
            RESTRICTED=\'password\\s*=\\s*.+\'
            git secrets --install
            git secrets --register-aws
            git secrets --add $RESTRICTED
            git secrets --scan
            if [ $? -eq 0 ]; then         echo "git secrets --scan OK";     else     echo "git secrets --scan FAIL"; fi
        '''
      }
    }
    }
    post {  
         failure {  
              mail bcc: '', body: "<b>Results</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL of build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "d.platisyne@gmail.com";   
         }
         success {  
              mail bcc: '', body: "<b>Results</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL of build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", to: "d.platisyne@gmail.com";   
         }
     }  
  }