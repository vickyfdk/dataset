pipeline {
	agent any
	stages {
		stage('Test run') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: 'Bione VPS', transfers: [sshTransfer(cleanRemote: false, excludes: '', 
				execCommand: '''php -v
				sudo /etc/init.d/apache2 restart''', 
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
				emailext attachLog: true, body: '', recipientProviders: [developers(), culprits()], subject: 'Jenkins Build Notiication - staging.bione.in', to: 'bdm@techwinst.com'
			}
		}
	}
	post {
		unstable {
			slackSend(color: '#dc3545', message: "Build Is Unstable ${env.JOB_NAME} ${env.BUILD_NUMBER}")
		}
		success {
			slackSend(color: '#28a745', message: "Build Is Successful ${env.JOB_NAME} ${env.BUILD_NUMBER}")
		}
	}
}