#!/usr/bin/env groovy
 
/**
        * Sample Jenkinsfile for Jenkins2 Pipeline
        * by shzshi 
 */
 
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL
 
try {
node {

def gradleHome

stage ('Clone Source Files') {
git : https://github.com/kyoayala/helloworld.git

// Get the Gradle tool.
// ** NOTE: This 'gradle' gradle tool must be configured
// **       in the global configuration. 
gradleHome = tool 'gradle'

}
stage ('gradle build') {
	
  if(isUnix()){
  sh "'${gradleHome}/bin/gradle' build --info"

  }
  else{
	bat ''${gradleHome}/bin/gradle' build --info'
  }
}

} // node
} // try end
catch (any) {

 currentBuild.result = "FAILURE"
 String recipient = 'shzshi@gmail.com'
 /*mail subject: "${env.JOB_NAME} (${env.BUILD_NUMBER}) failed",
         body: "It appears that ${env.BUILD_URL} is failing, somebody should do something about that",
           to: recipient,
      replyTo: recipient,
 from: 'noreply@mysite' */
 throw any
 
} finally {
  
 /*(currentBuild.result != "ABORTED") && node("master") {
     // Send e-mail notifications for failed or unstable builds.
     // currentBuild.result must be non-null for this step to work.
     step([$class: 'Mailer',
        notifyEveryUnstableBuild: true,
        recipients: "${email_to}",
        sendToIndividuals: true])
 }*/
}