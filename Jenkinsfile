#!groovy

import groovy.json.JsonSlurperClassic

node {
    def BUILD_NUMBER = env.BUILD_NUMBER
	def RUN_ARTIFACT_DIR = "tests/${BUILD_NUMBER}"
	def SFDC_USERNAME
    def HUB_ORG=env.HUB_ORG
    
    def SFDC_HOST=env.SFDC_HOST_DH
    def JWT_KEY_CRED_ID=env.JWT_KEY_CRED_ID_DH
     def CONNECTED_APP_CONSUMER_KEY = env.CONNECTED_APP_CONSUMER_KEY_DH
	 
   println 'KEY IS'
   println 'JWT_KEY_CRED_ID'
   println 'HUB_ORG'
   println 'SFDC_HOST'
   println 'CONNECTED_APP_CONSUMER_KEY'
   
   
    stage('checkout source') {
        checkout scm
    }
	
	  
        withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {

            // -------------------------------------------------------------------------
            // Authorize the Dev Hub org with JWT key and give it an alias.
            // -------------------------------------------------------------------------

            stage('Authorize ORG') {
			if(isUnix()){
                rc = sh returnStatus: true , script : "sfdx force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${jwt_key_file} -d --instanceurl ${SFDC_HOST}"
                }
				else{
				rc = bat returnStatus: true , script : "sfdx force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${jwt_key_file} -d --instanceurl ${SFDC_HOST}"
            }
			
			if(rc != 0)
			{
			error 'hub org authorization failed'
			}
			println(rc)
			}
			}
}
