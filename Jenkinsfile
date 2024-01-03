node("maven-builds")
{
 stage("SCM Checkout")
 {
  checkout scm
  mvnHome = tool 'M3'
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
