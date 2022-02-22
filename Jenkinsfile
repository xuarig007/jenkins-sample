// Powered by Infostretch 

timestamps {

	node () {

		stage ('App-IC - Checkout') {
		 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/xuarig007/jenkins-sample']]]) 
		}
		stage ('App-IC - Build') {
				// Maven build step
			withMaven(maven: 'maven') { 
				if(isUnix()) {
					sh "mvn clean package " 
				} else { 
					bat "mvn clean package " 
				} 
			} 
		}
		stage('Test') {
			withMaven(maven: 'maven') {
				bat 'mvn test'
			}
		}
		stage(' Quality check') {
			withSonarQubeEnv('Sonar') {
				bat "mvn sonar:sonar"
			}
		}
		stage ('App-IC - Post build actions') {
			// Mailer notification
			step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'stephane.rigaux@gmail.com', sendToIndividuals: false])

		}
	}
}
