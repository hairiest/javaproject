pipeline {
	agent {
		label 'master' }
	
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
		stage('Deploy') {
			steps {
			sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
}
}
}
	post {

		always {
			archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true

 }

	}
}
