pipeline {
	agent any

	stages {

		stage('Build') {
			steps {
			sh '/opt/ant/bin/ant -f build.xml -v' }
		}
}

	post {

		always {
			archive 'dist/*.jar'

 }

	}
}
