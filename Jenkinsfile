pipeline {
	agent any
	stages {
		stage('Test run') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: 'Bione VPS', transfers: [sshTransfer(cleanRemote: false, excludes: '', 
				execCommand: '''cd /home 
				sudo php -v''', 
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
				slackSend channel: 'jenkins-deployment-logs', color: 'good', message: 'Jenkins deployment Build is successful', tokenCredentialId: 'slack-ID'
			}
		}
	}

}
