pipeline {
	agent any
	stages {
		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'OWASP'
			}
		}
	}

	post {
		always {
      recordIssues enabledForFailure: true, tool: sonarQube()
    }
		success {
			dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
		}
	}
}
