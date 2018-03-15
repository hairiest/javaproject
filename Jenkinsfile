pipeline {
	agent any
	





	stages {
		stage('UNit Test') {
			steps {
			sh 'ant -f test.xml -v'
			junit 'reports/result.xml'
}}
		stage('Build') {
			steps {
			sh '/opt/ant/bin/ant -f build.xml -v' }
		}
}

	post {

		always {
			archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true

 }

	}
}
