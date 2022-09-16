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
       mail to: 'devops@acme.com',
    subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input",
    body: "Please go to ${BUILD_URL} and verify the build"
    } 
    unsuccessful {
        // send the error mail
        echo " Unsuccessful"
    }
}
}
