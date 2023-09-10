def dockerImage;

node('DockerBI'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/menaNosshy/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('menaNosshy/agent-dnc:v' + env.BUILD_NUMBER, './Dotnetcore');
	}
	stage('push'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds'){
			dockerImage.push();
		}
	}
}


