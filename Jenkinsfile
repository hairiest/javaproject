pipeline {
	agent  none
	
	stages {
		stage('UNit Test') {
			agent {

				label 'apache'
}
			steps {
			sh 'ant -f test.xml -v'
			junit 'reports/result.xml'
}}
		stage('Build') {
			agent {
				label 'apache' }
			steps {
			sh '/opt/ant/bin/ant -f build.xml -v' }
		}

		 post {

               success {
                        archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true

 }

        }

		stage('Deploy') {
			agent {
				label 'apache' }
			steps {
			sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
}
}
		stage('RUnning on Centos'){
			agent {
				label 'centos' }
			steps {
			sh "wget http://192.168.1.254/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar "
			sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
				}
}
}
}
