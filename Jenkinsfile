node {
	def app
	stage('Clone reposotiry'){
		checkout scm
	}
	stage('Build image'){
		app = docker.build("redbfs/jenkins-blueocean-part")
	}
	stage('Push image'){
		docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
	}
}
