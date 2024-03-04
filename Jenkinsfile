pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
{
 stage("SCM Checkout")
 {
  checkout scm
  mvnHome = '/opt/apache-maven-3.9.4/'
 }

 stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      archive 'target/*.war'
   }
   stage('deploy') {
   		sh "cp -p **/*.war /opt/tomcat/webapps"
   }
   	  
}
