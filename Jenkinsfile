pipeline {
	agent any
	stages {
		stage('Test run') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: 'Bione VPS', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home
sudo touch vickyfdk.txt''', execTimeout: 12000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
			}
		}
	}

}
