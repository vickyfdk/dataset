pipeline {
	agent any
	stages {
		stage('Test run') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: 'Bione VPS', transfers: [sshTransfer(cleanRemote: false, excludes: '', 
				execCommand: '''php -v''', 
				execTimeout: 12000, 
				flatten: false, 
				makeEmptyDirs: false, 
				noDefaultExcludes: false, 
				patternSeparator: '[, ]+', 
				remoteDirectory: '', 
				remoteDirectorySDF: false, 
				removePrefix: '', sourceFiles: '')], 
				usePromotionTimestamp: false, 
				useWorkspaceInPromotion: false, 
				verbose: false)])
				//slackSend channel: 'jenkins-deployment-logs', color: '#439FE0', message: "${env.JOB_NAME} ${env.BUILD_NUMBER}", tokenCredentialId: 'slack-ID'
				
			}
		}
	post {
        failure {
            script {
                if (BUILDING_TAG == 'yes') {
                    slackSend(color: '#dc3545', message: "Error publishing")
                }
            }
        }

        success {
            script {
                if (BUILDING_TAG == 'yes') {
                    slackSend(color: '#28a745', message: "Published")
                }
            }
        }	
	}

}
}
