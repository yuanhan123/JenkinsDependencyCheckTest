pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				// put ur github link
				git 'https://github.com/yuanhan123/simple-node-js-react-npm-app.git'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
