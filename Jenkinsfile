pipeline {
agent {label 'JDK11'}
options {
        timeout(time: 1, unit: 'HOURS')
        retry(3)
        }
triggers {
cron('0 * * * *') }
stages{ 
  stage ( 'source code' ){
    steps {
        git (url: 'https://github.com/Sandip090/spring-petclinic.git', branch: 'main')
    }
  } 
  stage ('Build the code'){
    steps {
        sh script: 'mvn clean package' 
  }
}
  stage ('Test case reports'){
    steps {
        junit testResults: 'target/surefire-reports/*.xml'
    }
  }
}
post {
    success {
        // send the success email
        echo "success"
        mail bcc: '', body: "Build success Build ID: ${BUID_ID}", cc: '', from: 'sandip123talk2me@gmail.com', replyTo: '', subject: "Job Url: ${JOB_URL} Test results: ${RUN_TESTS_DISPLAY_URL}",
         to: 'sandipsahoo009@gmail.com'
    } 
    unsuccessful {
        // send the error mail
        echo " Unsuccessful"
    }
}
}
