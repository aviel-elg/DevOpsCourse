node {
    def newApp
    def registry = 'https://registry-1.docker.io/v2/'
	def imagename = "aviel98/aviel_todo_java_app"
    def registryCredential = 'bdf53ea7-030e-4b20-8f81-640f53ab341a'
	
	stage('Git') {
		git 'https://github.com/aviel98/DevOpsCourse.git'
	}
	stage('Build') {
		nodejs(nodeJSInstallationName: 'NodeJS') { 
			sh label: '', script: '''
			cd src
			npm audit fix
			npm install --only=dev
			'''
			}
	}
	stage('Test') {
		nodejs(nodeJSInstallationName: 'NodeJS') { 
			sh label: '', script: '''
			npm test
		'''
		}
	}
	stage('Building image') {
        docker.withRegistry( registry, registryCredential ) {
		    def buildName = imagename + ":$BUILD_NUMBER"
			newApp = docker.build(buildName)
			newApp.push();
        }
	}
}