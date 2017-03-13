#!/usr/bin/env groovy
 
/**
        * Jenkinsfile for Jenkins2 Pipeline
        * 
*/
 
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL
 
try {
node {
     def buildNumber = '0.1.0'

	stage ('Clone Source Files')
	checkout scm

	stage ('Gradle Build & Assemble') {

		  if(isUnix()){
		  sh './gradlew clean build assemble'
		  }
		  else{
			bat './gradlew.bat clean build assemble'
		  }
	}
	
	stage ('Finger Printing Artifact') {
	
		sh "openssl md5 ${WORKSPACE}/build/libs/gs-gradle-${buildNumber}.jar"
		sh 'sed -i "s/md5.*/md5: \"$(openssl md5 gs-gradle-${buildNumber}.jar | awk \'{print $2}\')\"/" ${WORKSPACE}/config/software/morpeus-ui.rb'
	}
	

} // node
} // try end
catch (any) {

 currentBuild.result = "FAILURE"
 String recipient = 'your@emailaddress.com'
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
        recipients: "your@emailaddress.com",
        sendToIndividuals: true])
 }*/
}