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
		 post {
               success {
                        archiveArtifacts artifacts: 'dist/*.jar' , fingerprint: true
 }
        }
}

		stage('Deploy') {
			agent {
				label 'apache' }
			steps {
			sh "mkdir /var/www/html/rectangles/all/${env.BRANCH_NAME}"
			sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}"
}
}
		stage('Running on Centos'){
			agent {
				label 'centos' }
			steps {
			sh "wget http://192.168.1.247/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.BUILD_NUMBER}.jar "
			sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
				}
}
		stage('Test on Debian') {
			
			agent {
				docker 'openjdk:8u151-jre'
		}
		steps {
			sh "wget http://192.168.1.247/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.BUILD_NUMBER}.jar "
			sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
				}}


		stage('Promote to Green'){
			agent {
			label 'apache'
}
		when {
			branch 'master'
		}
		steps {

			sh "cp /var/www/html/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/green/rectangle_${env.BUILD_NUMBER}.jar"
			}


}
		stage('Promote development to master') {

			agent {

				label 'apache' }
			when {
				branch 'development' }

			steps {
			echo "stashing any local changes"
			sh "git stash"
			echo "checking out development branch"
			sh "git checkout development"
			echo "checking out the master branch"
			sh "git checkout master"
			echo "merging development into master branch"
			sh "git merge development"
			echo "Pushing to origin master"
			sh "git push origin master"
			

}			
}			
}
}
