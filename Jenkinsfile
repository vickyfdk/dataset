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
				
  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"
  def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)

  emailext(
      subject: subject,
      body: details,
      recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
			}
		}
	}

}
